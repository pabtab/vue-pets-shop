<template>
  <div class="hello">
    <b-container class="bx-example-row">
      <b-row>
        <b-col cols="4" v-for="pet in pets" v-bind:key="pet.id">
          {{pet.context.name}}
          <div>
            <b-card
              :title="pet.context.name"
              :img-src="pet.context.image"
              img-top
              tag="article"
              style="max-width:20rem;"
              class="mb-2">
            <p class="card-text">
              {{pet.context.description}}
            </p>
            <b-button href="#" variant="primary">
              Adoptar
            </b-button>

            </b-card>
          </div>
        </b-col>
      </b-row>
      <b-form @submit="postPet">
        <b-form-group id="name"
                      label="Nombre de la mascota:"
                      label-for="name"
                      description="Agregue la descripcion de la mascota">
            <b-form-input id="name"
                          type="text"
                          v-model="form.name"
                          required>
            </b-form-input>
        </b-form-group>
        <b-form-group id="image"
                      label="Url de la foto"
                      label-for="image"
                      description="Agregue la url de la foto">
            <b-form-input id="image"
                          type="text"
                          v-model="form.image"
                          required>
            </b-form-input>
        </b-form-group>
        <b-form-group id="description"
                      label="Agregue descricion"
                      label-for="desc"
                      description="Agregue la descripncion de la mascota">
          <b-form-input id="description"
                          type="text"
                          v-model="form.description"
                          required>
          </b-form-input>
        </b-form-group>
        <b-button type="submit" variant="primary">Agregar mascota</b-button>
      </b-form>
    </b-container>
  <h1></h1>
    
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },

  data() {
    return {
      pets: [],
      form: {
        name: '',
        image: '',
        description: ''
      },
    };
  },

  mounted() {
    axios
      .get(
        "http://things.ubidots.com/api/v1.6/devices/pets/petlist/values?token=A1E-uWcVqarOPgqJFhY2cqFTexdECgWGcX"
      )
      .then(response => {
        this.pets = response.data.results;
      });
  },

  methods: {
    postPet() {
      console.log(this.form)
      //debugger
      const data = {
        value: 0,
        context: {
          name: this.form.name,
          image: this.form.image,
          description: this.form.description
        }
      };
      debugger
      axios
        .post(
          "http://things.ubidots.com/api/v1.6/devices/pets/petlist/values?token=A1E-uWcVqarOPgqJFhY2cqFTexdECgWGcX",
          data
        )
        .then(response => {
          console.log(response.status);
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
