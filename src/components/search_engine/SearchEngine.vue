<template>
    <div class="cont">
        <div class="contenido">
        <div class="ipb">
            <label for="Ciudad">Ciudad</label>
            <div class="input">
                <input v-model="ciudad" type="text">
            </div>
            <button class="btn btn-dark" @click="fetchCiudad(ciudad)">Buscar ciudad</button>
            <button @click="mostrarCiudades"> Mostrar ciudades </button>
            <button @click="limpiarCiudades"> Borrar todo</button>

            </div>
            <div class="nombre">
                {{ nombre }}
            </div>
        </div>
        <div class="container">
        <div class="row">
          <div v-for="city in ciudades" :key="city.location.name" class="col-md-4 mb-4">
            <div class="cartas my-3"> <!-- Agregado el margen vertical (my-3) -->
              <CardComponent
                :icon="city.current.weather_icons[0]"
                :ciudad="city.location.name"
                :pais="city.location.country"
                :temperature="city.current.temperature"
                :weather="city.current.weather_descriptions[0]"
                :pressure="city.current.pressure"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script setup>
    import { defineProps, ref } from 'vue';
    import CardComponent from '../card/CardComponent.vue';
    
    let urlCiudad = (ciudad) => `http://api.weatherstack.com/forecast?access_key=2a64fa12c4f65875d6d3ea04326e0618&query=${ciudad}`



    const addCiudad = (a) => {
        if (!('success' in a == false)) {
            let obj  = {
                current: {
                    temperature: '0°: ni frio ni calor',
                    weather_icons: ['https://cdn-icons-png.flaticon.com/512/57/57108.png'], 
                    weather_descriptions: ['No se sabe'],
                    pressure: 'No se sabe'
                },
                location: {
                    name: 'Desconocido',
                    country: 'No se sabe'
                }
            }
            ciudades.value.push(obj);
            } else if (!ciudades.value.some(ciudad => ciudad.location.name === a.location.name)) {
                ciudades.value.push(a);
            }
    };

    const fetchData = async (a) => {
        try 
        {
            const response = await fetch(a);
            const json = await response.json();
            console.log(json);
            return json;
        }
        catch (err)
        {
            console.error(err)
        }
    }

    const fetchCiudad = async (a) => {
        try 
        {
            const response = await fetchData(urlCiudad(a))
            addCiudad(response);
        }
        catch (err)
        {
            console.error(err)
        }
    }

    
    const mostrarCiudades = () => console.log(ciudades.value);

    const limpiarCiudades = () => ciudades.value = [];

    let ciudad = ref('')

    let ciudades = ref([])

    

</script>
<style>
    button {
        margin-top: 10px;
    }
    .ipb {
        display:flex;
        flex-direction: column;
        justify-content: center;
        text-align: center;
    }
    label {
        font-size: 130%;
        margin-bottom: 10px 
    }
    .cont{
        display: flex;
        flex-direction: column;
    }
    .cartas{
        display: inline-block;
    }
</style>