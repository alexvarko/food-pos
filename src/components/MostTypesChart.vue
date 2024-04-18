<template>
  <div class="chart">

    <div class="pie" style="--p: 100;--c:#353440;--b:10px;">

      <div class="pie" style="--p: 75;--c:#65B0F6;--b:10px; z-index: 999;">
        <div class="pie" style="--p: 100;--c:#2A2836;--b:10px; --w:220px">
          <div class="pie" style="--p: 50;--c:#FFB572;--b:10px; --w:220px; z-index: 999;">
            <div class="pie" style="--p: 100;--c:#353440;--b:10px; --w:200px;">
          <div class="pie" style="--p: 65;--c:#FF7CA3;--b:10px; --w:200px; z-index: 999;">
            <div class="pie" style="--p: 100;--c:#2A2836;--b:10px; --w:180px">

            </div>
          </div>
          </div>
        </div>
        </div>
      </div>

    </div>


  </div>
</template>

<script lang="ts">

</script>


<style lang="scss" scoped>
.pie {
  --p: 20;
  --b: 22px;
  --c: darkred;
  --w: 240px;

  width: var(--w);
  aspect-ratio: 1;
  position: relative;
  display: inline-grid;
  place-content: center;
  font-size: 25px;
  font-weight: bold;
  font-family: sans-serif;
}

.pie:before,
.pie:after {
  content: "";
  position: absolute;
  border-radius: 50%;
}

.pie:before {
  inset: 0;
  background:
    radial-gradient(farthest-side, var(--c) 98%, #0000) top/var(--b) var(--b) no-repeat,
    conic-gradient(var(--c) calc(var(--p)*1%), #0000 0);
  -webkit-mask: radial-gradient(farthest-side, #0000 calc(99% - var(--b)), #000 calc(100% - var(--b)));
  mask: radial-gradient(farthest-side, #0000 calc(99% - var(--b)), #000 calc(100% - var(--b)));
}

.pie:after {
  inset: calc(50% - var(--b)/2);
  background: var(--c);
  transform: rotate(calc(var(--p)*3.6deg)) translateY(calc(50% - var(--w)/2));
}
</style>