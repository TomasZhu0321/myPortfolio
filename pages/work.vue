<template>
  <div>
    <canvas ref="canvas"></canvas>

    <div>
      <div
        id="workPage"
        class="absolute text-white text-center"
        style=" top:20% transform: translate(-50%, -50%);left: 40%"
      >
        <h1
          id="thomaswork"
          class="font-space-mono text-6xl tracking-wide"
          style="transform: translateY(30px)"
        >
          My work
        </h1>
        <section
          class="grid-column: 2 / 8; padding: 1rem; background: var(--dark-bg); font-size: 1.25rem; line-height: 1.5; margin-bottom: var(--spacing);"
        >
          <br />
          <h2>👩🏽‍🚀 E-commerce</h2>

          <ul>
            <li>
              ✅Built E-commerce front-end web page based on React.js framework;
              users can sort the display according to letters or prices on the
              product page; the fuzzy search function of the product is
              implemented; and the product can be further filtered by color,
              price, company and other tags to pinpoint the user needs and
              enhance the user experience
            </li>
            <li>
              ✅Fetched furniture API using Axios; controlled the upper limit of
              adding to the shopping cart by stock on the product detail page
              and display it in real time in the shopping cart; used FormSpree
              to manage the user input e-mail.
            </li>
            <li>
              ✅Implemented authentication and authorization using Auth0
              enhancing the security of user information and supporting Google
              account login.
            </li>
            <li>
              ✅Added checkout function via Stripe payments infrastructure and
              deployed to Netlify serverless platform.
            </li>
          </ul>
          <iframe
            width="560"
            height="315"
            src="https://www.youtube.com/embed/1cnhJRoDjcI"
            title="YouTube video player"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </section>
        <section
          class="grid-column: 2 / 8; padding: 1rem; background: var(--dark-bg); font-size: 1.25rem; line-height: 1.5; margin-bottom: var(--spacing);"
          style="right: 40%"
        >
          <br />
          <h2>👩🏽‍🚀 Hamilton Rent</h2>

          <ul>
            <li>
              ✅Built a Full-Stack Event-Based dynamic website that allows
              tenants to view rental information based on the map and rate and
              leave comments on the rental properties; landlords can register
              and then upload information about the rooms.
            </li>
            <li>
              ✅Set up front-ed view engine using Embedded JavaScript(EJS) with
              HTML/CSS/JS; achieved responsive layout through Bootstrap5; added
              Joi package for scheme validation, and deployed it to
              Heroku(PaaS).
            </li>
            <li>
              ✅Implemented RESTful APIs to handle HTTP requests and responses
              using Express.js and Node.js; designed primary database with
              MongoDB; utilized Cloudinary to privide image storage; achieved
              user authentication through Passport.
            </li>
            <li>
              ✅Integrated MapBox's APIs to generate a cluter map of
              accommodations based on geocode and display the location on
              dynamic map
            </li>
          </ul>
          <iframe
            width="560"
            height="315"
            src="https://www.youtube.com/embed/EeJG19qkZ5s"
            title="YouTube video player"
            frameborder="0"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
          ></iframe>
        </section>
        <section
          class="grid-column: 2 / 8; padding: 1rem; background: var(--dark-bg); font-size: 1.25rem; line-height: 1.5; margin-bottom: var(--spacing);"
          style="right: 40%"
        >
          <br />
          <h2>👩🏽‍🚀 Personal Website</h2>

          <ul>
            <li>
              ✅Designed and implemented 3D dynamic interactive personal website
              based on Three.js and Nuxt.js; rendered the layout of the pages
              via Tailwind CSS; deployed it on personal website using Netlify.
            </li>
            <li>
              ✅Captured mouse in real time and displayed the light in the
              corresponding position of the background plate; realized the real
              time deformation of the background page through the dat.gui;
            </li>
            <li>
              ✅Simulated trigonometric waveform and applied to achieve the
              undirected rhythm of the background plate.
            </li>
            <li>
              ✅Added animation effect to text through gsap to improve visual
              experience; and realized amzaing transition effect by transforming
              camera position; added each project effect display video in
              personal achievement displ
            </li>
          </ul>
        
        </section>
      </div>
    </div>
    <!-- <canvas ref="canvas"></canvas> -->
    <!-- <div class="bg-black h-screen">
      <h2>asdfsda</h2>
    </div> -->
  </div>
</template>

<script>
import {
  PlaneGeometry,
  BoxGeometry,
  ConeGeometry,
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
  TorusKnotGeometry,
  MeshStandardMaterial,
  PointLightHelper,
  GridHelper,
  SphereGeometry,
  MeshBasicMaterial,
  MathUtils,
  TextureLoader,
} from "three";
import OrbitControls from "orbit-controls-es6";
// import * as dat from "dat.gui";
import gsap from "gsap";

export default {
  mounted() {
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

    renderer.setPixelRatio(window.devicePixelRatio);
    renderer.setSize(window.innerWidth, window.innerHeight);
    camera.position.setZ(400);
    // camera.position.setY(70);

    renderer.render(scene, camera);

    //sphere + box 1
    const sphe = new SphereGeometry(5, 14, 6);
    const material = new MeshBasicMaterial({ color: 0x4d68ff });
    const sphere = new Mesh(sphe, material);
    sphere.position.set(180, 90, 80);
    scene.add(sphere);

    const box = new BoxGeometry(50, 50, 50);
    const boxMaterial = new MeshBasicMaterial({
      color: 0xffffff,
      wireframe: true,
    });
    const cube = new Mesh(box, boxMaterial);
    cube.position.set(180, 90, 80);
    scene.add(cube);

    //sphere + box 1
    const sphe2 = new SphereGeometry(5, 14, 6);
    const material2 = new MeshBasicMaterial({ color: 0xffff00 });
    const sphere2 = new Mesh(sphe2, material2);
    sphere2.position.set(-280, -190, -180);
    scene.add(sphere2);

    const box2 = new BoxGeometry(90, 90, 90);
    const boxMaterial2 = new MeshBasicMaterial({
      color: 0xffffff,
      wireframe: true,
    });
    const cube2 = new Mesh(box2, boxMaterial2);
    cube2.position.set(-280, -190, -180);
    scene.add(cube2);

    //sphere + box 1
    const sphe3 = new SphereGeometry(5, 14, 6);
    const material3 = new MeshBasicMaterial({ color: 0xf23f00 });
    const sphere3 = new Mesh(sphe3, material3);
    sphere3.position.set(-150, 145, 80);
    scene.add(sphere3);

    const box3 = new BoxGeometry(90, 90, 90);
    const boxMaterial3 = new MeshBasicMaterial({
      color: 0xffffff,
      wireframe: true,
    });
    const cube3 = new Mesh(box3, boxMaterial3);
    cube3.position.set(-150, 145, 80);
    scene.add(cube3);

    const knot = new TorusKnotGeometry(50, 2, 8, 12, 5, 8);
    const knotmaterial = new MeshBasicMaterial({
      color: 0xffb74d,
      wireframe: true,
    });
    const torusKnot = new Mesh(knot, knotmaterial);
    torusKnot.position.set(0, 100, -250);
    scene.add(torusKnot);
    //Thomas

    const ThomasTexture = new TextureLoader().load("me.png");
    const skinTexture = new TextureLoader().load("normal.png");
    const thomas = new Mesh(
      new SphereGeometry(70, 70, 70),
      new MeshBasicMaterial({ map: ThomasTexture, normalMap: skinTexture })
    );
    thomas.position.set(-200, 10, -200);
    scene.add(thomas);
    function moveCamera() {
      const t = document.body.getBoundingClientRect().top;
      thomas.rotation.x += 0.02;
      thomas.rotation.y += 0.075;
      //   thomas.rotation. += 0.05;
      thomas.position.x -= 0.05;
      thomas.position.z -= 0.05;
      thomas.position.y -= 0.3;

      camera.position.z = t * -0.001;
      camera.position.x = t * -0.001;
      camera.rotation.y = t * -0.005;
    }

    document.body.onscroll = moveCamera;
    moveCamera();

    // const lightHelper = new PointLightHelper(pointLight);
    // const gridHelper = new GridHelper(200, 50);
    // scene.add(lightHelper, gridHelper);
    // const controls = new OrbitControls(camera, renderer.domElement);

    const starGeometry = new BufferGeometry();
    const starMaterial = new PointsMaterial({
      color: 0xffffff,
    });
    const starVerticies = [];
    for (let i = 0; i < 20000; i++) {
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
    addEventListener("resize", () => {
      camera.aspect = innerWidth / innerHeight;
      camera.updateProjectionMatrix();
      renderer.setSize(innerWidth, innerHeight);
    });

    // const spaceTexture = new TextureLoader().load("space.jpg");
    // scene.background = spaceTexture;

    // const ThoamsTexture = new TextureLoader().load("me.png");
    // const Thomas = new Mesh(
    //   new SphereGeometry(10, 80, 80),
    //   new MeshBasicMaterial({ map: ThoamsTexture })
    // );
    // Thomas.position.set(18, 15, 8);
    // scene.add(Thomas);

    // const ThoamsTexture2 = new THREE.TextureLoader().load('me2.jpg');
    // const Thomas2 = new THREE.Mesh(
    //   new THREE.SphereGeometry(4,40,40),
    //   new MeshBasicMaterial({map:ThoamsTexture2})
    // )
    // Thomas2.position.set(-20,19,5);
    // scene.add(Thomas2);

    // const ThoamsTexture3 = new THREE.TextureLoader().load('me3.jpg');
    // const Thomas3= new THREE.Mesh(
    //   new THREE.SphereGeometry(5,50,50),
    //   new THREE.MeshBasicMaterial({map:ThoamsTexture3})
    // )
    // Thomas3.position.set(10,-10,-10);
    // scene.add(Thomas3);

    function animate() {
      requestAnimationFrame(animate);
      torusKnot.rotation.y += 0.02;
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.005;
      cube.rotation.z += 0.005;

      sphere.rotation.x += 0.01;
      sphere.rotation.y += 0.005;
      sphere.rotation.z += 0.005;

      cube2.rotation.x += 0.01;
      cube2.rotation.y += 0.005;
      cube2.rotation.z += 0.005;

      cube3.rotation.x += 0.005;
      cube3.rotation.y += 0.02;
      cube3.rotation.z += 0.005;
      sphere2.rotation.x += 0.01;
      sphere2.rotation.y += 0.005;
      sphere2.rotation.z += 0.005;
      //   corn.rotation.x += 0.01;
      //   corn.rotation.y += 0.005;
      //   corn.rotation.z += 0.005;

      //   controls.update();
      renderer.render(scene, camera);
      stars.rotation.x += 0.0005;
    }
    animate();
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
