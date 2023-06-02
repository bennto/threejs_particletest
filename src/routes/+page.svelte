<script>
  import {
    Canvas,
    InstancedMesh,
    Instance,
    Object3DInstance,
    useThrelte,
    T,
    OrbitControls,
    PerspectiveCamera,
  } from "@threlte/core";
  import { BoxBufferGeometry, MeshStandardMaterial } from "three";
  import { useGltf, GLTF } from "@threlte/extras";

  const { gltf } = useGltf("src/lib/assets/brain_low_poly/scene.gltf");
  $: brain = $gltf?.nodes["Brain_Brain_0"];
  $: cerebellum = $gltf?.nodes["cerebellum_cerebellum_0"];
  $: medulla = $gltf?.nodes["medulla_medulla_0"];

  function randNum(i) {
    return Math.ceil(Math.random() * i) * (Math.round(Math.random()) ? 1 : -1);
  }
  const rotation = (90 * Math.PI) / 180;

  let basicGeom = new BoxBufferGeometry(1, 1, 1);
  const basicMat = new MeshStandardMaterial({ color: "black" });
</script>

<div class="scene">
  <Canvas>
    <!-- Camera -->
    <PerspectiveCamera position={{ x: 0, y: 0, z: 300 }} fov={50}>
      <OrbitControls enableZoom enableRotate />
    </PerspectiveCamera>

    <T.AmbientLight color="black" intensity={1} />

    {#if gltf}
      <T.Mesh geometry={brain.geometry} material={basicMat} />
      <T.Mesh geometry={cerebellum.geometry} material={basicMat} />
    {/if}

    <!-- Sphere -->
    <!-- <InstancedMesh geometry={brain.geometry} material={basicMat}>
      <Instance position={{ x: randNum(160), y: randNum(90), z: 0 }} />
    </InstancedMesh> -->
  </Canvas>
</div>

<style>
  .scene {
    width: 100%;
    height: 100%;
    position: absolute;
    inset: 0;
    background: #ffcaca;
    background-attachment: fixed;
  }
</style>
