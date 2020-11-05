<template>
  <v-app>
    <v-img src="@/assets/fondito.jpg" aspect-ratio="10">
      <v-container class="fill-height">
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <v-card class="elevation-12">
              <v-window v-model="step">
                <v-window-item :value="1">
                  <v-row>
                    <v-col cols="12" md="8">
                      <v-card-text>
                        <h1 class="display-1 ml-5">Inicio de sesión</h1>
                        <v-form>
                          <v-text-field
                            class="ml-5 mr-5 mt-5"
                            label="Email"
                            v-model="email"
                            prepend-icon="mdi-account-circle-outline"
                            type="text"
                          />
                          <v-text-field
                            class="ml-5 mr-5 mt-3"
                            id="password"
                            label="Contraseña"
                            v-model="password"
                            prepend-icon="mdi-lock-outline"
                            type="password"
                          />
                        </v-form>
                        <h3 class=" subtitle-2 ml-13 primary--text">
                          ¿Olvidaste tu contraseña?
                        </h3>
                      </v-card-text>
                      <div class="text-center mt-5 mb-5">
                        <v-btn
                          color="primary"
                          class="elevation-5"
                          @click="submit"
                          >Iniciar sesion</v-btn
                        >
                      </div>
                    </v-col>
                    <v-col
                      cols="12"
                      md="4"
                      class="primary d-flex flex-column justify-space-between"
                    >
                      <v-card-text class="mt-5">
                        <h1 class="text-center display-1 white--text">
                          ¿Todavía no tenés una cuenta?
                        </h1>
                      </v-card-text>
                      <div class="text-center mb-5">
                        <v-btn
                          color="white"
                          class="elevation-5 primary--text"
                          dark
                          @click="step++"
                          >Registrarse</v-btn
                        >
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="2">
                  <v-row>
                    <v-col
                      cols="12"
                      md="4"
                      class="primary d-flex flex-column justify-space-between"
                    >
                      <v-card-text class=" mt-5">
                        <h1 class="text-center display-1 white--text">
                          ¿Ya tenés una cuenta?
                        </h1>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn
                          color="white"
                          class="elevation-5 primary--text mb-5"
                          @click="step--"
                          >Iniciar sesión</v-btn
                        >
                      </div>
                    </v-col>
                    <v-col cols="12" md="8">
                      <v-card-text>
                        <h1 class="display-1 mt-5 ml-5">Registro</h1>
                        <v-form>
                          <v-text-field
                            class="ml-5 mr-5 mt-5"
                            label="Dirección de mail"
                            v-model="email"
                            prepend-icon="mdi-email-outline"
                            type="text"
                          />
                          <v-text-field
                            class="ml-5 mr-5 mt-1"
                            label="Nombre"
                            v-model="name"
                            prepend-icon="mdi-account-circle-outline"
                            type="text"
                          />
                          <v-text-field
                            class="ml-5 mr-5 mt-1"
                            id="password"
                            label="Contraseña"
                            v-model="password"
                            prepend-icon="mdi-lock-outline"
                            type="password"
                          />
                          <v-text-field
                            class="ml-5 mr-5 mt-1"
                            id="password"
                            label="Confirmar contraseña"
                            v-model="password2"
                            prepend-icon="mdi-lock-outline"
                            type="password"
                          />
                        </v-form>
                      </v-card-text>
                      <div class="text-center mt-1 mb-5">
                        <v-btn
                          color="primary"
                          class="elevation-5"
                          @click="submitForm"
                          dark
                          >Registrarse</v-btn
                        >
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-img>
  </v-app>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    step: 1,
    return: {
      email: "",
      name: "",
      password: "",
      password2: "",
      edit: true
    }
  }),

  computed: {
    currentTitle() {
      switch (this.step) {
        case 1:
          return "Signin";
        case 2:
          return "Signup";
      }
    }
  },

  methods: {
    /*no sé hacerlo funcionar :C*/

    submit() {
      axios
        .get(
          "http://54.80.18.229:8123/api/Usuarios/getByEmailAndPassword",
          {
            params: {
              email: this.email,
              password: this.password
            }
          },
          {
            auth: {
              username: "PF2020",
              password: "PF2020APIv1"
            }
          }
        )
        .then((response) => {
          console.log(response);
        })

        .catch((error) => {
          console.log(error);
        });
    },

    submitForm() {
      axios
        .post("http://54.80.18.229:8123/api/Usuarios/Registrar", {
          email: this.email,
          name: this.name,
          password: this.password,
          edit: this.edit
        })
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    }
  }
};
</script>
