<template>
<html>
<body>
   <div class="dropdown-container">
            <h2>Indonesia</h2>
            <div class="dropdown-provinsi">
                <span>Provinsi</span>
                <select v-model="selectedContinent">
                    <option value="">Pilih Provinsi</option>
                    <option v-for="(country_obj, country) in places" :value="country" :key="country_obj">{{country}}</option>
                </select>
            </div>
            <div class="dropdown-kota">
                <span>Kota</span>
                <select :disabled="countries.length == 0" v-model="selectedCountry">
                    <option value="">Pilih Kabupaten</option>
                    <option v-for="(city_obj, city) in countries" :value="city" :key="city_obj">{{city}}</option>
                </select>
            </div>
            <div class="dropdown-kecamatan">
                <span>Kecamatan</span>
                <select :disabled="cities.length == 0" v-model="selectedCity">
                    <option value="">Pilih Kecamatan</option>
                    <option v-for="city in cities" :value="city" :key="city">{{city}}</option>
                </select>
            </div>
        </div>
</body>
</html>
</template>

<script>
export default {
  data: function () {
    return {
      places: {
        "Jakarta": {
          Cilegon: ['Ciwandan', 'Citangkil', 'Pulomerak', 'Purwakarta'],
          Serang: ['Curug', 'Walantaka', 'Serang', 'Kasemen'],
          Pandeglang: ['Labuan', 'Carita', 'Cimanuk', 'Bojong']
        },
        "Jawa Timur": {
          Tuban: ['Jenu', 'Tuban', 'Rengel', 'Kerek'],
          Malang: ['Lowokwaru', 'Arjosari', 'Klojen'],
        }
      },
      countries: [],
      cities: [],
      selectedContinent: '',
      selectedCountry: '',
      selectedCity: ''
    }
  },
  watch: {
    selectedContinent: function () {
      // Clear previously selected values
      this.countries = []
      this.cities = []
      this.selectedCountry = ''
      this.selectedCity = ''
      // Populate list of countries in the second dropdown
      if (this.selectedContinent.length > 0) {
        this.countries = this.places[this.selectedContinent]
      }
    },
    selectedCountry: function () {
      // Clear previously selected values
      this.cities = []
      this.selectedCity = ''
      // Now we have a continent and country. Populate list of cities in the third dropdown
      if (this.selectedCountry.length > 0) {
        this.cities = this.places[this.selectedContinent][this.selectedCountry]
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
  min-height: 100%;
  min-width: 100%;
  position: fixed;
  top: 0;
  left: 0;
}
h2 {
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
  color: white;
}
.dropdown-container {
  display: inline-block;
  width: 300px;
  height: 250px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #808080;
  color: #4c3f54;
  border-radius: 15px;
  padding: 20px;
  box-shadow:  2px 8px 8px 2px rgba(0,0,0,0.0);
}
.dropdown-provinsi, .dropdown-provinsi span{
padding: 10px;
}
.dropdown-kota , .dropdown-kota span{
  padding: 10px;
}
.dropdown-kecamatan , .dropdown-kecamatan span{
  padding: 10px;
}
.text-hasil span {
  font-size: 20px;
}
</style>
