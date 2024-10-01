<template>
  <div class="szakkor-card animacio" style="animation-delay: 2s">
    <div class="szakkor-header">
      <h2>{{ szakkor.nev }}</h2>
      <span
        >(Tagok:
        <span class="tagokSzama"> {{ tanulokCsoportja.length }} </span>)</span
      >
    </div>
    <div v-if="tanulokCsoportja.length > 0" class="szakkor-gyerekek">
      <span
        v-for="(tanulo, i) in tanulokCsoportja"
        :key="tanulo.id"
        class="black"
      >
        {{ tanulo.nev }}
        <span v-if="i < tanulokCsoportja.length - 1" class="bar"> | </span>
      </span>
    </div>
    <div v-else class="szakkor-nincs-tanulo">
      <span>Nincs beiratkozott gyerek.</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["szakkor", "tanulok"],
  computed: {
    tanulokCsoportja() {
      return this.tanulok
        .filter((t) => t.szakkorId == this.szakkor.id)
        .sort((a, b) => a.nev.localeCompare(b.nev));
    },
  },
};
</script>

<style scoped>
.szakkor-card {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 15px;
  width: 100%;
  background-color: #f9f9f9;
}

.szakkor-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #ddd;
  padding-bottom: 10px;
  margin-bottom: 10px;
}

.szakkor-header h2 {
  margin: 0;
  font-size: 1.1em;
  color: #333;
}

.szakkor-header span {
  font-size: 0.9em;
  color: #666;
}

.szakkor-gyerekek ul {
  list-style-type: none;
  padding: 0;
}

.szakkor-gyerekek span {
  padding: 5px 0;
  color: var(--color);
  font-size: 1.1em;
}

.black {
  color: #000 !important;
}

.szakkor-nincs-tanulo {
  font-style: italic;
  color: var(--color);
}

.tagokSzama {
  color: var(--color) !important;
  font-weight: bold;
}

.bar {
  color: var(--color);
  text-shadow: 0 0 10px var(--color), 0 0 20px var(--color),
    0 0 22px var(--color);
}
</style>