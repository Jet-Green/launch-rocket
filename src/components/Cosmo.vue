<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from "gsap/ScrollTrigger";

import * as THREE from 'three';


onMounted(() => {
    const scene = new THREE.Scene();

    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
    camera.lookAt(0, 0, 0)

    const renderer = new THREE.WebGLRenderer({
        canvas: document.querySelector('#bg'),
    })

    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);

    camera.position.setZ(document.body.getBoundingClientRect().top)

    const ambientLight = new THREE.AmbientLight(0xffffff)
    scene.add(ambientLight)

    function addStar() {
        const geometry = new THREE.SphereGeometry(0.2, 24, 24)
        const material = new THREE.MeshStandardMaterial({ color: 0xffffff })
        const star = new THREE.Mesh(geometry, material)
        const [x, y, z] = Array(3).fill().map(() => THREE.MathUtils.randFloatSpread(300))

        star.position.set(x, y, z)
        scene.add(star)
    }

    for (let i = 0; i < 400; i++) {
        addStar()
    }

    function moveCamera() {
        const t = document.body.getBoundingClientRect().top
        gsap.to(camera.position, {
            z: t * -0.02,
            duration: 2,
            ease: 'power3.out'
        })
    }
    document.body.onscroll = moveCamera

    function animate() {
        requestAnimationFrame(animate)
        renderer.render(scene, camera)
    }

    animate()


    gsap.registerPlugin(ScrollTrigger);
    // let titleTl = gsap.timeline()
    // titleTl.to('.main-title', {
    //     opacity: 0,
    // })
    // titleTl.to('.main-title', {
    //     opacity: 1,
    // })
    // ScrollTrigger.create({
    //     animation: titleTl,
    //     trigger: '.title-card',
    //     start: 'top top',
    //     markers: true,
    //     // scrub: 1,
    //     pin: true,
    //     // anticipatePin: 1,
    // })


    let tl1 = gsap.timeline()
    tl1.to('.first-card', {
        opacity: 1,
        duration: 0.5,
    })
    tl1.to('.first-card', {
        opacity: 0,
        duration: 0.5,
    }, '+=2')

    ScrollTrigger.create({
        animation: tl1,
        trigger: '.first-card',
        start: 'top 25%',
        end: '+=275%',
        markers: true,
        scrub: true,
        pin: true,
        anticipatePin: 1,
    })

    let tl2 = gsap.timeline()
    tl2.to('.second-card', {
        opacity: 1,
        duration: 0.5,
    })
    tl2.to('.second-card', {
        opacity: 0,
        duration: 0.5,
    }, "+=2")

    ScrollTrigger.create({
        animation: tl2,
        trigger: '.second-card',
        start: 'top 25%',
        end: '+=275%',
        markers: true,
        scrub: true,
        pin: true,
        anticipatePin: 1,
    })
})

</script>
<template>
    <v-row class="bg-black">
        <v-col cols="12">
            <canvas id="bg"></canvas>
            <v-row class="main-content">
                <v-col cols="12" class="title-card">
                    <div class="main-title">
                        <h1 class="text-center">Персональная страница Савелия Шутова</h1>
                    </div>
                </v-col>
                <v-col cols="12" class="first-card">
                    <v-row>
                        <v-col cols="1">
                        </v-col>
                        <v-col cols="6">
                            <v-card class="message-card rounded-lg">
                                <!-- Lorem ipsum dolor sit amet consectetur,
                                adipisicing
                                elit. Est
                                praesentium amet minima quidem
                                aut id quam accusantium hic, illo aperiam temporibus sapiente eius quod facere. Animi
                                autem fuga
                                odit soluta! -->
                                <v-skeleton-loader type="table-heading, list-item-two-line, image"></v-skeleton-loader>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-col>
                <v-col cols="12" class="second-card">
                    <v-row>
                        <v-col cols="5">
                        </v-col>
                        <v-col cols="6">
                            <v-card class="message-card rounded-lg">
                                <!-- Lorem ipsum dolor sit amet consectetur,
                                adipisicing
                                elit. Est
                                praesentium amet minima quidem
                                aut id quam accusantium hic, illo aperiam temporibus sapiente eius quod facere. Animi
                                autem fuga
                                odit soluta! -->
                                <v-skeleton-loader type="table-heading, list-item-two-line, image"></v-skeleton-loader>
                            </v-card>
                        </v-col>
                    </v-row>
                </v-col>
                <v-col cols="12" class="third-card">

                </v-col>
            </v-row>
        </v-col>
    </v-row>
</template>
<style lang="scss" scoped>
canvas {
    position: fixed;
    top: 0;
    left: 0;
}

.main-content {
    position: absolute;
    width: 100%;
}

.title-card {
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.message-card {
    padding: 16px;
}

.first-card {
    height: 300vh;
    opacity: 0;
}

.second-card {
    height: 300vh;
    opacity: 0;
}

.third-card {
    height: 300vh;
    opacity: 0;
}
</style>