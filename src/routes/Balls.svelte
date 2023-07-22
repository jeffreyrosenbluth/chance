<script lang="ts">
	import P5, { type Sketch, type p5 } from 'p5-svelte';
	import type Vector from 'p5-svelte';
	import type Color from 'p5-svelte';

	export let names: Array<string>;
	$: n = names.length;

	let width = 800;
	let height = 800;
	const radius = 35;

	class Ball {
		p: p5;
		pos: Vector;
		vel: Vector;
		radius: number;
		color: Color;
		name: string;

		constructor(p: p5, pos: Vector, vel: Vector, radius: number, color: Color, name: string) {
			this.p = p;
			this.pos = pos;
			this.vel = vel;
			this.radius = radius;
			this.color = color;
			this.name = name;
		}

		collide(other: Ball) {
			if (other == this) {
				return;
			}
			let relative = this.p.Vector.sub(other.pos, this.pos);
			let dist = relative.mag() - (this.radius + other.radius);
			if (dist < 0) {
				let movement = relative.copy().setMag(this.p.abs(dist / 2));
				this.pos.sub(movement);
				other.pos.add(movement);

				let thisToOtherNormal = relative.copy().normalize();
				let approachSpeed = this.p.max(
					this.p.min(this.vel.dot(thisToOtherNormal) + -other.vel.dot(thisToOtherNormal), 10),
					5
				);
				let approachVector = thisToOtherNormal.copy().setMag(approachSpeed);
				this.vel.sub(approachVector);
				other.vel.add(approachVector);
			}
		}

		move() {
			this.pos.add(this.vel);
			if (this.pos.x < this.radius) {
				this.pos.x = this.radius;
				this.vel.x = -this.vel.x;
			}
			if (this.pos.x > width - this.radius) {
				this.pos.x = width - this.radius;
				this.vel.x = -this.vel.x;
			}
			if (this.pos.y < this.radius) {
				this.pos.y = this.radius;
				this.vel.y = -this.vel.y;
			}
			if (this.pos.y > height - this.radius) {
				this.pos.y = height - this.radius;
				this.vel.y = -this.vel.y;
			}
		}

		gone() {
			let center = this.p.createVector(width / 2, height / 2);
			let relative = this.p.Vector.sub(center, this.pos);
			let dist = relative.mag() - this.radius * 2;
			return dist < 0;
		}

		render() {
			this.p.noFill();
			this.p.stroke(this.color);
			this.p.strokeWeight(3);
			this.p.ellipse(this.pos.x, this.pos.y, 2 * this.radius);
			this.p.fill(this.color);
			this.p.noStroke();
			this.p.textSize(28);
			this.p.textAlign(this.p.CENTER);
			this.p.text(this.name, this.pos.x, this.pos.y + 10);
		}
	}

	let balls: Array<Ball> = [];

	const sketch: Sketch = (p5) => {
		p5.setup = () => {
			p5.createCanvas(width, height);
			for (let i = 0; i < n; i++) {
				balls.push(
					new Ball(
						p5,
						p5.createVector(p5.random(width), p5.random(height)),
						p5.Vector.random2D().mult(3 + p5.random(7)),
						radius,
						p5.color(p5.random(255), p5.random(255), p5.random(255)),
						names[i]
					)
				);
			}
		};

		p5.draw = () => {
			p5.background(p5.color(0));
			p5.noStroke();
			p5.fill(255, 65, 0, 80);
			const x = width / 2;
			const y = height / 2;
			let diameter = 2 * radius;

			if (balls.length > 1) {
				for (let i = 0; i < 5; i++) {
					p5.ellipse(x, y, diameter, diameter);
					diameter = diameter / 1.8;
				}
			}

			let bs = balls.filter((e) => !e.gone());
			balls = balls.length === 1 ? balls : bs;

			for (let i = 0; i < balls.length; i++) {
				for (let j = 0; j < i; j++) {
					balls[i].collide(balls[j]);
				}
			}

			for (let i = 0; i < balls.length; i++) {
				balls[i].move();
				balls[i].render();
			}
		};
	};
</script>

<P5 {sketch} />
