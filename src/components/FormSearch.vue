<script setup>
import {computed, reactive, ref} from "vue";

const city_names = reactive(["Aberdeen", "Abilene", "Akron", "Albany", "Albuquerque", "Alexandria", "Allentown", "Amarillo", "Anaheim", "Anchorage", "Ann Arbor", "Antioch", "Apple Valley", "Appleton", "Arlington", "Arvada", "Asheville", "Athens", "Atlanta", "Atlantic City", "Augusta", "Aurora", "Austin", "Bakersfield", "Baltimore", "Barnstable", "Baton Rouge", "Beaumont", "Bel Air", "Bellevue", "Berkeley", "Bethlehem", "Billings", "Birmingham", "Bloomington", "Boise", "Boise City", "Bonita Springs", "Boston", "Boulder", "Bradenton", "Bremerton", "Bridgeport", "Brighton", "Brownsville", "Bryan", "Buffalo", "Burbank", "Burlington", "Cambridge", "Canton", "Cape Coral", "Carrollton", "Cary", "Cathedral City", "Cedar Rapids", "Champaign", "Chandler", "Charleston", "Charlotte", "Chattanooga", "Chesapeake", "Chicago", "Chula Vista", "Cincinnati", "Clarke County", "Clarksville", "Clearwater", "Cleveland", "College Station", "Colorado Springs", "Columbia", "Columbus", "Concord", "Coral Springs", "Corona", "Corpus Christi", "Costa Mesa", "Dallas", "Daly City", "Danbury", "Davenport", "Davidson County", "Dayton", "Daytona Beach", "Deltona", "Denton", "Denver", "Des Moines", "Detroit", "Downey", "Duluth", "Durham", "El Monte", "El Paso", "Elizabeth", "Elk Grove", "Elkhart", "Erie", "Escondido", "Eugene", "Evansville", "Fairfield", "Fargo", "Fayetteville", "Fitchburg", "Flint", "Fontana", "Fort Collins", "Fort Lauderdale", "Fort Smith", "Fort Walton Beach", "Fort Wayne", "Fort Worth", "Frederick", "Fremont", "Fresno", "Fullerton", "Gainesville", "Garden Grove", "Garland", "Gastonia", "Gilbert", "Glendale", "Grand Prairie", "Grand Rapids", "Grayslake", "Green Bay", "GreenBay", "Greensboro", "Greenville", "Gulfport-Biloxi", "Hagerstown", "Hampton", "Harlingen", "Harrisburg", "Hartford", "Havre de Grace", "Hayward", "Hemet", "Henderson", "Hesperia", "Hialeah", "Hickory", "High Point", "Hollywood", "Honolulu", "Houma", "Houston", "Howell", "Huntington", "Huntington Beach", "Huntsville", "Independence", "Indianapolis", "Inglewood", "Irvine", "Irving", "Jackson", "Jacksonville", "Jefferson", "Jersey City", "Johnson City", "Joliet", "Kailua", "Kalamazoo", "Kaneohe", "Kansas City", "Kennewick", "Kenosha", "Killeen", "Kissimmee", "Knoxville", "Lacey", "Lafayette", "Lake Charles", "Lakeland", "Lakewood", "Lancaster", "Lansing", "Laredo", "Las Cruces", "Las Vegas", "Layton", "Leominster", "Lewisville", "Lexington", "Lincoln", "Little Rock", "Long Beach", "Lorain", "Los Angeles", "Louisville", "Lowell", "Lubbock", "Macon", "Madison", "Manchester", "Marina", "Marysville", "McAllen", "McHenry", "Medford", "Melbourne", "Memphis", "Merced", "Mesa", "Mesquite", "Miami", "Milwaukee", "Minneapolis", "Miramar", "Mission Viejo", "Mobile", "Modesto", "Monroe", "Monterey", "Montgomery", "Moreno Valley", "Murfreesboro", "Murrieta", "Muskegon", "Myrtle Beach", "Naperville", "Naples", "Nashua", "Nashville", "New Bedford", "New Haven", "New London", "New Orleans", "New York", "New York City", "Newark", "Newburgh", "Newport News", "Norfolk", "Normal", "Norman", "North Charleston", "North Las Vegas", "North Port", "Norwalk", "Norwich", "Oakland", "Ocala", "Oceanside", "Odessa", "Ogden", "Oklahoma City", "Olathe", "Olympia", "Omaha", "Ontario", "Orange", "Orem", "Orlando", "Overland Park", "Oxnard", "Palm Bay", "Palm Springs", "Palmdale", "Panama City", "Pasadena", "Paterson", "Pembroke Pines", "Pensacola", "Peoria", "Philadelphia", "Phoenix", "Pittsburgh", "Plano", "Pomona", "Pompano Beach", "Port Arthur", "Port Orange", "Port Saint Lucie", "Port St. Lucie", "Portland", "Portsmouth", "Poughkeepsie", "Providence", "Provo", "Pueblo", "Punta Gorda", "Racine", "Raleigh", "Rancho Cucamonga", "Reading", "Redding", "Reno", "Richland", "Richmond", "Richmond County", "Riverside", "Roanoke", "Rochester", "Rockford", "Roseville", "Round Lake Beach", "Sacramento", "Saginaw", "Saint Louis", "Saint Paul", "Saint Petersburg", "Salem", "Salinas", "Salt Lake City", "San Antonio", "San Bernardino", "San Buenaventura", "San Diego", "San Francisco", "San Jose", "Santa Ana", "Santa Barbara", "Santa Clara", "Santa Clarita", "Santa Cruz", "Santa Maria", "Santa Rosa", "Sarasota", "Savannah", "Scottsdale", "Scranton", "Seaside", "Seattle", "Sebastian", "Shreveport", "Simi Valley", "Sioux City", "Sioux Falls", "South Bend", "South Lyon", "Spartanburg", "Spokane", "Springdale", "Springfield", "St. Louis", "St. Paul", "St. Petersburg", "Stamford", "Sterling Heights", "Stockton", "Sunnyvale", "Syracuse", "Tacoma", "Tallahassee", "Tampa", "Temecula", "Tempe", "Thornton", "Thousand Oaks", "Toledo", "Topeka", "Torrance", "Trenton", "Tucson", "Tulsa", "Tuscaloosa", "Tyler", "Utica", "Vallejo", "Vancouver", "Vero Beach", "Victorville", "Virginia Beach", "Visalia", "Waco", "Warren", "Washington", "Waterbury", "Waterloo", "West Covina", "West Valley City", "Westminster", "Wichita", "Wilmington", "Winston", "Winter Haven", "Worcester", "Yakima", "Yonkers", "York", "Youngstown"]);

const cities = reactive(city_names.map(city => ({
  label: city,
  select: false
})))

const searchString = ref('');

const isOnlySelected = ref(false);

const showCities = computed(() => {
  if(searchString.value && isOnlySelected.value) {
    return cities.filter(city => city.label.includes(searchString.value) && city.select);
  }

  if(searchString.value) {
    return cities.filter(city => city.label.includes(searchString.value));
  }

  if(isOnlySelected.value) {
    return cities.filter(city => city.select);
  }

  return cities
})

const selectCity = (city) => {
  const findCity = cities.find(item => item.label === city.label)
  findCity.select = !findCity.select
}

const clearAll = () => {
  cities.forEach((item, index) => cities[index].select = false)
  searchString.value = '';
  isOnlySelected.value = false;
}

const save = () => {
  console.log('Save city = ', cities.filter(city => city.select))
}
</script>

<template>
  <div class="search-form">
    <input
        v-model="searchString"
        class="search-form__input"
        type="text"
        placeholder="Search"
    >
    <span class="search-form__divider" />
    <div class="d-flex justify-space-between search-form__switch-wrapper">
      <div
          class="d-flex align-center gap-4"
      >
        <label class="switch">
          <input v-model="isOnlySelected" type="checkbox">
          <span class="slider round"></span>
        </label>
        <label
            class="search-form__switch-label cursor-pointer"
            @click="isOnlySelected = !isOnlySelected"
        >
          Show selected only
        </label>
      </div>
      <p class="search-form__clear-all cursor-pointer" @click="clearAll">
        Clear all
      </p>
    </div>
    <ul class="pa-0 my-0 search-form__city-list">
      <li
          v-for="(city, index) in showCities"
          :key="index"
          class="search-form__city-list-item d-flex align-center gap-3 pa-1 cursor-pointer"
          @click="selectCity(city)"
      >
        <label class="container-checkbox">
          <input
              v-model="city.select"
              type="checkbox">
          <span
              class="checkbox-checkmark"
              @click="selectCity(city)"
          ></span>
        </label>
        <span>{{ city.label }}</span>
      </li>
    </ul>
    <span class="search-form__divider" />
    <div class="d-flex justify-end">
      <button
          class="search-form__button"
          @click="save"
      >
        Save
      </button>
    </div>
  </div>
</template>

<style scoped lang="scss">
$main-color: #232323;

.search-form {
  display: flex;
  flex-direction: column;
  width: 500px;

  padding: 16px 20px;
  background: #FFFFFF;
  border: 1px solid #E1E3E6;
  box-shadow: 9px 32px 35px rgba(0, 0, 0, 0.0464653);
  border-radius: 14px;
  box-sizing: border-box;

  @media screen and (max-width: 620px) {
    width: 100%;
  }

  &__switch-wrapper {
    @media screen and (max-width: 620px) {
      flex-direction: column;
    }
  }

  &__input {
    color: #343434;
    font-weight: 475;
    font-size: 16px;
    line-height: 19px;
    letter-spacing: -0.5px;

    margin: 0;
    padding: 0;
    border: none;
    background: none;
    font-family: inherit;
    outline: none;
    box-shadow: none;
    appearance: none;
    &::-webkit-input-placeholder {
      color: inherit;
      opacity: 0.9;
    }
    &::-moz-placeholder {
      color: inherit;
      opacity: 0.5;
    }
    &:-ms-input-placeholder {
      color: inherit;
      opacity: 0.5;
    }
    &::-ms-input-placeholder {
      color: inherit;
      opacity: 0.5;
    }
  }

  &__divider {
    margin: 8px 0;
    height: 1px;
    background: #ECECEC;
  }

  &__switch-label {
    font-weight: 550;
    font-size: 16px;
    line-height: 22px;
    letter-spacing: -0.5px;
    color: $main-color;
  }

  &__clear-all {
    font-weight: 550;
    font-size: 16px;
    line-height: 22px;
    letter-spacing: -0.5px;
    color: $main-color;
  }

  &__city-list {
    height: 240px;
    display: flex;
    flex-direction: column;
    gap: 12px;
    overflow-y: auto;

    &::-webkit-scrollbar {
      width: 8px;

    }

    &::-webkit-scrollbar-track {
      background: none;
    }

    &::-webkit-scrollbar-thumb {
      background: #888;
      border-radius: 4px;
    }

    &::-webkit-scrollbar-thumb:hover {
      background: #555;
    }
  }

  &__button {
    position: relative;
    cursor: pointer;
    display: inline-block;
    padding: 8px 25px;
    background: #60D09B;
    color: #FFFFFF;
    border-radius: 16px;
    border: none;

    &:hover {
      background: #66d29e;
    }

    &:after {
      content: "";
      position: absolute;
      left: 0;
      top: 0;
      right: 0;
      bottom: 0;
      width: 100%;
      height: 100%;
      border-radius: 16px;
      opacity: 0;
      transition: all 0.5s;
      box-shadow: 0 0 5px 5px hsl(154, 51%, 57%);
    }

    &:active:after {
      box-shadow: 0 0 0 0 #4ea67d;
      opacity: 0.75;
      transition: 0s;
    }
  }
}

.container-checkbox {
  width: 22px;
  height: 22px;
  display: block;
  position: relative;

  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.container-checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkbox-checkmark {
  position: absolute;
  top: 0;
  left: 0;
  width: 22px;
  height: 22px;
  border-radius: 8px;
  background-color: #eee;
}

.container-checkbox:hover input ~ .checkbox-checkmark {
  background-color: #ccc;
}

.container-checkbox input:checked ~ .checkbox-checkmark {
  background-color: #2196F3;
}

.checkbox-checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.container-checkbox input:checked ~ .checkbox-checkmark:after {
  display: block;
}

.container-checkbox .checkbox-checkmark:after {
  left: 7px;
  top: 3px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}

.switch {
  position: relative;
  display: inline-block;
  width: 40px;
  height: 22px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 15px;
  width: 15px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(17px);
  -ms-transform: translateX(17px);
  transform: translateX(17px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>