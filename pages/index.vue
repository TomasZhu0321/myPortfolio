<template>
  <div>
    <canvas ref="canvas"></canvas>
    <div id="app">
      <div
        id="beginPage"
        class="absolute text-white text-center"
        style="top: 50%; transform: translate(-50%, -50%); left: 50%"
      >
        <p
          id="thomas"
          class="font-space-mono text-3xl tracking-wide opacity-0 "
          style="transform: translateY(30px)"
        >
          DEMING(THOMAS) ZHU
    </p>
        <p
          id="goal"
          class="font-exo text-6xl font-extrabold italic uppercase mt-3 opacity-0"
        >
          A gradute student hunting for Co-op
        </p>
        <p id="date" class="font-exo text-2xl uppercase mt-3 opacity-0">
          (jan.2023-Sep.2023)
          <br />
          <button
            id="viewWork"
            class="border py-2 px-4 rounded-lg text-m font-space-mono uppercase mt-5 hover:bg-white hover:text-gray-800 opacity-0"
          >
            View work
          </button>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import {
  PlaneGeometry,
  BufferAttribute,
  Raycaster,
  Scene,
  PerspectiveCamera,
  WebGLRenderer,
  MeshPhongMaterial,
  DoubleSide,
  Mesh,
  DirectionalLight,
  PointLight,
  BufferGeometry,
  PointsMaterial,
  Float32BufferAttribute,
  Points,
} from "three";

// import * as dat from "dat.gui";
import gsap from "gsap";

// import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls'
import OrbitControls from 'orbit-controls-es6';
export default {
  mounted() {
    const dat = require("dat.gui");
    const gui = new dat.GUI();
    const world = {
      plane: {
        width: 500,
        height: 500,
        widthSegments: 130,
        heightSegments: 130,
      },
    };
    gui.add(world.plane, "width", 1, 800).onChange(generatePlane);
    gui.add(world.plane, "height", 1, 800).onChange(generatePlane);
    gui.add(world.plane, "widthSegments", 1, 500).onChange(generatePlane);
    gui.add(world.plane, "heightSegments", 1, 500).onChange(generatePlane);
    function generatePlane() {
      planeMesh.geometry.dispose();
      planeMesh.geometry = new PlaneGeometry(
        world.plane.width,
        world.plane.height,
        world.plane.widthSegments,
        world.plane.heightSegments
      );
      const { array } = planeMesh.geometry.attributes.position;
      const randomValues = [];
      for (let i = 0; i < array.length; i++) {
        if (i % 3 === 0) {
          const x = array[i];
          const y = array[i + 1];
          const z = array[i + 2];
          array[i] = x + (Math.random() - 0.5) * 3;
          array[i + 1] = y + (Math.random() - 0.5) * 3;
          array[i + 2] = z + (Math.random() - 0.5) * 8;
        }
        randomValues.push(Math.random() * Math.PI * 2);
      }
      planeMesh.geometry.attributes.position.randomValues = randomValues;
      planeMesh.geometry.attributes.position.originalPostion =
      planeMesh.geometry.attributes.position.array;

      const colors = [];
      for (let i = 0; i < planeMesh.geometry.attributes.position.count; i++) {
        colors.push(0.192, 0.192, 0.192);
      }
      //!!add new attribute to geomertry
      planeMesh.geometry.setAttribute(
        "color",
        new BufferAttribute(new Float32Array(colors), 3)
      );
    }
    const raycaster = new Raycaster(); //when mouse move, the ray point to the plane
    const scene = new Scene(); //container

    const camera = new PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new WebGLRenderer({
      canvas: this.$refs.canvas,
    });
    renderer.setSize(innerWidth, innerHeight);
    renderer.setPixelRatio(devicePixelRatio);

    camera.position.z = 50;

    // orbit control
    new OrbitControls(camera, renderer.domElement);

    //default place Geomeotry
    const planeGeometry = new PlaneGeometry(500, 500, 130, 130);
    const planeMaterial = new MeshPhongMaterial({
      color: 0xc0c0c0,
      side: DoubleSide,
      flatShading: true,
      vertexColors: true,
    });
    const planeMesh = new Mesh(planeGeometry, planeMaterial);
    scene.add(planeMesh);

    generatePlane();
    // add light
    const light = new DirectionalLight(0xffffff, 1);
    light.position.set(0, 0, 1);
    scene.add(light);

    const pointLight = new PointLight(0xffffff);
    pointLight.position.set(0, 0, 1);
    scene.add(pointLight);
    const backlight = new DirectionalLight(0x3498db, 1);
    backlight.position.set(0, 0, -1);
    scene.add(backlight);

    //build stars
    const starGeometry = new BufferGeometry();
    const starMaterial = new PointsMaterial({
      color: 0xffffff,
    });
    const starVerticies = [];
    for (let i = 0; i < 10000; i++) {
      const x = (Math.random() - 0.5) * 2000;
      const y = (Math.random() - 0.5) * 2000;
      const z = (Math.random() - 0.5) * 2000;
      starVerticies.push(x, y, z);
    }
    starGeometry.setAttribute(
      "position",
      new Float32BufferAttribute(starVerticies, 3)
    );
    const stars = new Points(starGeometry, starMaterial);
    scene.add(stars);

    const mouse = {
      x: undefined,
      y: undefined,
    };

    let frame = 0;
    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);
      raycaster.setFromCamera(mouse, camera);
      frame += 0.01;
      const { array, originalPostion, randomValues } =
        planeMesh.geometry.attributes.position;
      for (let i = 0; i < array.length; i += 3) {
        array[i] =
          originalPostion[i] + Math.cos(frame + randomValues[i]) * 0.02;
        array[i + 1] =
          originalPostion[i + 1] + Math.sin(frame + randomValues[i + 1]) * 0.02;
        //  array[i+2] = originalPostion[i+2] + Math.cos(frame) * 0.003;
      }
      planeMesh.geometry.attributes.position.needsUpdate = true;

      const intersects = raycaster.intersectObject(planeMesh);
      if (intersects.length > 0) {
        const { color } = intersects[0].object.geometry.attributes;
        //vertice 1
        color.setX(intersects[0].face.a, 1);
        color.setY(intersects[0].face.a, 1);
        color.setZ(intersects[0].face.a, 1);
        //vertice 2
        color.setX(intersects[0].face.b, 1);
        color.setY(intersects[0].face.b, 1);
        color.setZ(intersects[0].face.b, 1);
        //vertice 3
        color.setX(intersects[0].face.c, 1);
        color.setY(intersects[0].face.c, 1);
        color.setZ(intersects[0].face.c, 1);

        intersects[0].object.geometry.attributes.color.needsUpdate = true;
        const initialColor = {
          r: 0.192,
          g: 0.192,
          b: 0.192,
        };
        const initialHoverColor = {
          r: 1,
          g: 1,
          b: 1,
        };

        gsap.to(initialHoverColor, {
          r: initialColor.r,
          g: initialColor.g,
          b: initialColor.b,
          onUpdate: () => {
            //vertice 1
            color.setX(intersects[0].face.a, initialHoverColor.r);
            color.setY(intersects[0].face.a, initialHoverColor.g);
            color.setZ(intersects[0].face.a, initialHoverColor.b);
            //vertice 2
            color.setX(intersects[0].face.b, initialHoverColor.r);
            color.setY(intersects[0].face.b, initialHoverColor.g);
            color.setZ(intersects[0].face.b, initialHoverColor.b);
            //vertice 3
            color.setX(intersects[0].face.c, initialHoverColor.r);
            color.setY(intersects[0].face.c, initialHoverColor.g);
            color.setZ(intersects[0].face.c, initialHoverColor.b);
            color.needsUpdate = true;
          },
        });
      }
      stars.rotation.x += 0.001;
    }
    animate();

    //listen the mouse move from user
    addEventListener("mousemove", (event) => {
      mouse.x = (event.clientX / innerWidth) * 2 - 1; //adjust X coordinates
      mouse.y = -(event.clientY / innerHeight) * 2 + 1; ////adjust Y coordinates
    });

    gsap.to("#thomas", {
      opacity: 1,
      duration: 1.5,
      delay: 0.3,
      y: 0,
      ease: "expo.in",
    });
    gsap.to("#goal", {
      opacity: 1,
      duration: 3,
    });
    gsap.to("#date", {
      opacity: 1,
      duration: 1.5,
      delay: 0.1,
      ease: "expo.in",
    });
    gsap.to("#viewWork", {
      opacity: 1,
      duration: 1.5,
      delay: 0.3,
    });

    document.querySelector("#viewWork").addEventListener("click", (event) => {
      event.preventDefault();
      gsap.to("#beginPage", {
        opacity: 0,
      });

      // gsap.to(camera.position, { z: 60, ease: "expo.inOut", duration: 2 });
      gsap.to(camera.position, { z: -30, ease: "expo.inOut", duration: 2 });
      gsap.to(camera.rotation, {
        x: -1.75,
        ease: "power3.inOut",
        duration: 2.5,
      });
      gsap.to(camera.position, {
        y: -1000,
        ease: "expo.in",
        duration: 1.5,
        delay: 2.5,
        onComplete: () => {
          
          window.location.href='https://thomasweb.netlify.app/';
        },
      });
    });

    addEventListener("resize", () => {
      camera.aspect = innerWidth / innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(innerWidth, innerHeight);
    });
  },
};
</script>

<style>
.font-exo {
  font-family: "Exo 2", sans-serif;
}
.font-space-mono {
  font-family: "Space Mono", monospace;
}
</style>