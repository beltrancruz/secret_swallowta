<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue';

const isReady = ref<boolean>(false)

const particlesLoaded = async (container: any) => {
	console.log("Particles container loaded", container);
};

const current = ref<number>(10)

const options = ref<any>({
	name: "Fireworks Mask",
	fullScreen: {
		enable: true
	},
	background: {
		color: "#000000",
		image: "url('https://www.xtrafondos.com/en/descargar.php?id=7888&resolucion=1920x1080')",
		// image: "url('https://wallpaperset.com/w/full/d/e/8/7662.jpg')",
		// image: "url('https://www.designyourway.net/blog/wp-content/uploads/2018/11/pastel-background-goo.jpg')",
		// image: "url('https://particles.js.org/images/background3.jpg')",
		position: "50% 50%",
		repeat: "no-repeat",
		size: "cover"
	},
	backgroundMask: {
		enable: true,
		cover: {
			color: "#000"
		}
	},
	emitters: {
		direction: "top",
		life: {
			count: 0,
			duration: 0.1,
			delay: 0.1
		},
		rate: {
			delay: 0.15,
			quantity: 1
		},
		size: {
			width: 100,
			height: 0
		},
		position: {
			y: 100,
			x: 50
		}
	},
	particles: {
		color: {
			value: "#fff"
		},
		number: {
			value: 0
		},
		destroy: {
			bounds: {
				top: 30
			},
			mode: "split",
			split: {
				count: 1,
				factor: {
					value: 0.333333
				},
				rate: {
					value: 100
				},
				particles: {
					stroke: {
						width: 0
					},
					color: {
						value: ["#ff595e", "#ffca3a", "#8ac926", "#1982c4", "#6a4c93"]
					},
					number: {
						value: 0
					},
					collisions: {
						enable: false
					},
					destroy: {
						bounds: {
							top: 0
						}
					},
					opacity: {
						value: {
							min: 0.1,
							max: 1
						},
						animation: {
							enable: true,
							speed: 0.7,
							sync: false,
							startValue: "max",
							destroy: "min"
						}
					},
					effect: {
						type: "trail",
						options: {
							trail: {
								length: {
									min: 5,
									max: 10
								}
							}
						}
					},
					shape: {
						type: "circle"
					},
					size: {
						value: 2,
						animation: {
							enable: false
						}
					},
					life: {
						count: 1,
						duration: {
							value: {
								min: 1,
								max: 2
							}
						}
					},
					move: {
						enable: true,
						gravity: {
							enable: true,
							acceleration: 9.81,
							inverse: false
						},
						decay: 0.1,
						speed: {
							min: 10,
							max: 25
						},
						direction: "outside",
						outModes: "destroy"
					}
				}
			}
		},
		life: {
			count: 1
		},
		effect: {
			type: "trail",
			options: {
				trail: {
					length: {
						min: 10,
						max: 30
					},
					minWidth: 1,
					maxWidth: 1
				}
			}
		},
		rotate: {
			path: true
		},
		shape: {
			type: "circle"
		},
		size: {
			value: 1
		},
		move: {
			enable: true,
			gravity: {
				acceleration: 15,
				enable: true,
				inverse: true,
				maxSpeed: 100
			},
			speed: {
				min: 10,
				max: 20
			},
			outModes: {
				default: "destroy",
				top: "none"
			}
		}
	},
	// sounds: {
	// 	enable: true,
	// 	events: [
	// 		{
	// 			event: "particleRemoved",
	// 			filter: (args: any) => args.data.particle.options.move.gravity.inverse,
	// 			audio: [
	// 				"https://particles.js.org/audio/explosion0.mp3",
	// 				"https://particles.js.org/audio/explosion1.mp3",
	// 				"https://particles.js.org/audio/explosion2.mp3"
	// 			]
	// 		}
	// 	],
	// 	volume: 50
	// }
})


onMounted(() => {
	const intervalId = setInterval(() => {
		if (current.value > 0) {
			current.value--;
		} else {
			clearInterval(intervalId);
		}
	}, 1500);

	onBeforeUnmount(() => {
		clearInterval(intervalId);
	});
})

</script>

<template>
	<main class="h-screen bg-[#000000] text-white font-sans select-none">
		<transition name="ready" mode="out-in">
			<section v-if="isReady" class="h-full w-full flex items-center justify-center relative">
				<div class="absolute top-0 left-0 z-10 w-full h-full flex flex-col justify-center items-center gap-4 font-bold">
					<div class="titan-one-regular bg-[linear-gradient(to_right,#F2AAFF,#F9E0F0,#E471FF,#FF86B9,#E2B0FF)] inline-block text-transparent bg-clip-text text-pretty text-8xl uppercase">
						Happy Birthday!
					</div>
					<h2 class="text-7xl italic"><span class="titan-one-regular ">Secret uwu</span> 🌺</h2>
				</div>
				<vue-particles class="z-0" id="tsparticles" @particles-loaded="particlesLoaded" :options="options" />
			</section>
			<section v-else class="h-full w-full flex items-center justify-center">
				<transition name="ready" mode="out-in">
					<button v-if="current == 0" @click="isReady = !isReady" type="button"
						class="hover:scale-105 transition duration-300 ease-in-out px-4 py-2 text-bold outline-none border-2 rounded-lg border-white">
						Trust me
					</button>
					<div v-else class="text-5xl">
						<transition name="pulse" mode="out-in">
							<p v-if="current == 10">10</p>
							<p v-else-if="current == 9">9</p>
							<p v-else-if="current == 8">8</p>
							<p v-else-if="current == 7">7</p>
							<p v-else-if="current == 6">6</p>
							<p v-else-if="current == 5">5</p>
							<p v-else-if="current == 4">4</p>
							<p v-else-if="current == 3">3</p>
							<p v-else-if="current == 2">2</p>
							<p v-else-if="current == 1">1</p>
							<p v-else="current == 0">0</p>
						</transition>
					</div>
				</transition>
			</section>
		</transition>
	</main>
</template>

<style scoped>
.ready-enter-active,
.ready-leave-active {
	transition: opacity 0.5s ease;
}

.ready-enter-from,
.ready-leave-to {
	opacity: 0;
}

.number {
  transition: opacity 0.5s ease-in-out;
  opacity: 1;
}

.number.is-fading-out {
  opacity: 0;
}

.pulse-enter-active,
.pulse-leave-active {
	transition: opacity 0.75s ease;
}

.pulse-enter-from,
.pulse-leave-to {
	opacity: 0;
}

.number {
  transition: opacity 0.5s ease-in-out;
  opacity: 1;
}

.number.is-fading-out {
  opacity: 0;
}

</style>
