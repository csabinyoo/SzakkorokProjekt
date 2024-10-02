<template>
  <div class="row">
    <div class="col-md-6 side-a">
      <h1>Táblázat</h1>
      <table class="table animacio my-table" style="animation-delay: 1s">
        <thead>
          <tr>
            <th>Név</th>
            <th>Osztály</th>
            <th>Szakkör</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="tanulo in tanulok" :key="tanulo.id">
            <td class="tabla-animacio">
              <i :class="noiNevuEAzIlleto(tanulo.nev)"></i>
              {{ tanulo.nev }}
            </td>
            <td class="tabla-animacio">{{ tanulo.osztaly }}</td>
            <td class="tabla-animacio">
              <select
                class="form-select"
                aria-label="Default select example"
                v-model="tanulo.szakkorId"
              >
                <option
                  v-for="szakkor in szakkorok"
                  :key="szakkor.id"
                  :value="szakkor.id"
                >
                  {{ szakkor.nev }}
                </option>
              </select>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="col-md-6 side-b">
      <div class="szakkor-lista">
        <h1>Szakkörök</h1>
        <tanuloKartya
          v-for="szakkor in szakkorok"
          :key="szakkor.id"
          :szakkor="szakkor"
          :tanulok="tanulok"
        />
      </div>
    </div>
  </div>
</template>

<script>
import tanuloKartya from "../components/tanuloKartya.vue";

export default {
  components: {
    tanuloKartya,
  },
  data() {
    return {
      tanulok: [
        { id: 1, nev: "Erős Anna", osztaly: "3a", szakkorId: 1 },
        { id: 2, nev: "Gyenge Pista", osztaly: "7b", szakkorId: 1 },
        { id: 3, nev: "Kis Pista", osztaly: "1a", szakkorId: 1 },
        { id: 4, nev: "Ledacs-Kiss Pista", osztaly: "8a", szakkorId: 1 },
        { id: 5, nev: "Tóth Mária", osztaly: "4c", szakkorId: 1 },
        { id: 6, nev: "Magyar Pista", osztaly: "9c", szakkorId: 1 },
        { id: 7, nev: "Német Katalin", osztaly: "2b", szakkorId: 1 },
        { id: 8, nev: "Oláh Pista", osztaly: "10b", szakkorId: 1 },
        { id: 9, nev: "Fehér Pista", osztaly: "11a", szakkorId: 1 },
        { id: 10, nev: "Fekete Eszter", osztaly: "13d", szakkorId: 1 },
      ],

      szakkorok: [
        { id: 1, nev: "Nincs szakkör" },
        { id: 2, nev: "Informatika" },
        { id: 3, nev: "Rajz" },
        { id: 4, nev: "Ének" },
        { id: 5, nev: "Kosárlabda" },
        { id: 6, nev: "Football" },
      ],
    };
  },
  methods: {
    noiNevuEAzIlleto(nev) {
      const noineiNevek = ["Anna", "Katalin", "Eszter", "Mária"];
      return noineiNevek.some((noiNev) => nev.includes(noiNev))
        ? "fa-regular fa-circle-user orange"
        : "fa-regular fa-circle-user text-color";
    },
  },
};
</script>

<style scoped>
.table {
  vertical-align: middle;
}

.table > :not(caption) > * > * {
  background-color: transparent;
  color: #fff;
}

.table thead tr {
  background-color: var(--color);
  text-align: left;
  font-weight: bold;
}

.table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.table tbody tr:nth-of-type(even) {
  background-color: #000;
}

.table tbody tr:last-of-type {
  border-bottom: 2px solid var(--color);
}

.szakkor-lista {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

.my-table thead th:first-child {
  border-top-left-radius: 10px !important;
}

.my-table thead th:last-child {
  border-top-right-radius: 10px !important;
}

.form-select:focus {
  -webkit-box-shadow: inset 0 0 0 transparent, 0 0 0 transparent;
  box-shadow: inset 0 0 0 transparent, 0 0 0 transparent;
}
</style>
