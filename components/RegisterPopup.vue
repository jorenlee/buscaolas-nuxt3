<script setup>
// import { mapGetters } from "vuex";
// export default {
//   data() {
//     return {
//       first_name: "",
//       last_name: "",
//       email: "",
//       password1: "",
//       password2: "",
//       telefono: "",
//       error: null,
//       PlanID: 3,
//       RegisterForm: true,
//       ValidatePhone: false,
//       ValidatePhoneAlertErrorToast: false,
//       CorrectionFormatAlertErrorToast: false,
//       CambiaTelefonoElements: false,
//       phone_number: "",
//       cambia_telefono: null,
//       region_select: null,
//       Regions: null,
//       user_id: null,
//       code: null,
//     };
//   },
//   async fetch() {
//     const DataRegion = await this.$axios.$get("/api/main/user/regiones/").then((res) => {
//       this.Regions = res;
//     });
//   },
//   computed: {
//     ...mapGetters(["isAuthenticated", "loggedInUser", "IsPremium"]),
//   },
//   methods: {
//     registerIni() {
//       this.RegisterForm = false;
//       this.$emit("CloseRegisterEvent");
//       this.$emit("OpenLogin");
//     },
//     async validated() {
//       try {
//         let code_response = await this.$axios.$post("/api/main/check-code/", {
//           user_id: this.user_id,
//           code: this.code,
//         });
//         if (code_response.success == true) {
//           const response_login = await this.$auth.loginWith("local", {
//             data: {
//               email: this.email.trim(),
//               password: this.password1,
//             },
//           });
//           this.$emit("CloseRegisterEvent");
//         } else {
//           this.ValidatePhoneAlertErrorToast = true;
//         }
//       } catch (e) {
//         this.$toast.error(e.response.data.detail);
//       }
//     },
//     async cambiarTelefono() {
//       try {
//         let response = await this.$axios.$put(
//           "/api/main/update-phone/" + this.user_id
//         );
//         this.$toast.success("El cambiar telefono");
//         this.ValidatePhone = true;
//         this.CambiaTelefonoElements = false;
//       } catch (e) {
//         this.$toast.error(e);
//       }
//     },
//     async register() {
//       try {
//         let response_register = await this.$axios.$post("/api/main/auth/register/", {
//           first_name: this.first_name,
//           last_name: this.last_name,
//           email: this.email.trim(),
//           password: this.password1,
//           password2: this.password2,
//           phone: this.telefono,
//           region: this.region_select,
//         });
//         this.user_id = response_register.id;
//         this.RegisterForm = false;
//         this.ValidatePhone = true;
//       } catch (e) {
//         if (!this.user_id) {
//           for (var i in e.response.data) {
//             for (var j in e.response.data[i]) {
//               this.$toast.error(i + ": " + e.response.data[i][j]);
//             }
//           }
//         } else {
//           this.$toast.error(e.response.status + ": algo paso, intentalo de nuevo");
//         }
//       }
//     },
//     Close() {
//       this.$emit("CloseRegisterEvent");
//     },
//   },
// };
</script>
<template>
  <div class="mx-auto w-800 bg-gradient mt-10">
    <div class="relative">
      <button
        class="absolute right-8 lg:top-7 top-16 block flex text-sm text-white leading-7"
        @click="Close()"
      >
        cerrar
        <span class="close-btn block ml-2"></span>
      </button>
      <img
        src="~/static/img/banner/surfing-VGSBTXB_3.png"
        class="w-800 h-474 lg:block hidden"
      />
    </div>
    <div class="lg:px-10 px-8 lg:pt-10 pt-5 lg:pb-16 pb-3">
      <div class="mx-auto text-white lg:w-min">
        <div class="mb-10" v-if="RegisterForm">
          <span
            class="leading-relaxed uppercase font-bold lg:text-4xl text-3xl mb-1 block lg:whitespace-nowrap"
            >REGISTRATE y hazte premium</span
          >
          <span class="uppercase lg:text-2xl text-xl font-light"
            >Para que cada sesión valga la pena</span
          >
          <span class="uppercase border-2 border-white mt-2 block w-24"></span>
          <p class="text-sm lg:hidden block mt-2"></p>
        </div>
        <div class="mb-10" v-if="ValidatePhone">
          <span
            class="leading-relaxed uppercase font-bold lg:text-4xl text-3xl mb-1 block lg:whitespace-nowrap"
            >Validemos tu teléfono</span
          >
          <span class="uppercase lg:text-2xl text-xl font-light"
            >Ingresa el código para validar tu teléfono</span
          >
          <span class="uppercase border-2 border-white mt-2 block w-24"></span>
          <p class="text-sm lg:hidden block mt-2">
            Hemos enviado un SMS al telefono {{ phone_number }}
          </p>
        </div>
        <div
          v-if="ValidatePhoneAlertErrorToast"
          class="flex mt-12 mb-10 items-center bg-red rounded-sm shadow"
        >
          <span class="alert-icon block ml-8 mr-6"></span>
          <p class="my-2 uppercase text-white text-base text-center tracking-widest">
            El Codigo no es valido
          </p>
        </div>
        <div
          v-if="CorrectionFormatAlertErrorToast"
          class="flex mt-12 mb-10 items-center bg-red rounded-sm shadow"
        >
          <span class="alert-icon block ml-8 mr-6"></span>
          <p class="my-2 uppercase text-white text-base text-center tracking-widest">
            El formato corrector es +56912312323
          </p>
        </div>
        <form class="lg:w-min mx-auto text-center" v-if="RegisterForm">
          <input
            placeholder="nombre"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2 mb-9"
            v-model="first_name"
            required
          />
          <input
            placeholder="apellido"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2 mb-9"
            v-model="last_name"
            required
          />
          <input
            placeholder="email"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2 mb-9"
            v-model="email"
            required
          />
          <input
            placeholder="contraseña"
            type="password"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2 mb-9"
            v-model="password1"
            autocomplete="new-password"
            required
          />
          <input
            placeholder="repite contraseña"
            type="password"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2 mb-9"
            v-model="password2"
            autocomplete="new-password"
            required
          />
          <select
            name="registerDropdown"
            id="registerDropdown"
            v-model="region_select"
            class="rounded-sm text-xs text-wide bg-white lg:w-80 w-full py-2 text-center uppercase text-dark-gray mb-9"
            required
          >
            <option value="" disabled selected>Region</option>
            <option v-for="reg in Regions" :key="reg.id" :value="reg.id">
              {{ reg.region }}
            </option>
          </select>
          <!-- pattern="[0-9]{3}-[0-9]{2}-[0-9]{3}" -->
          <input
            placeholder="Telefono"
            type="tel"
            id="telefono"
            name="telefono"
            class="block uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-full py-2"
            pattern="+[0-9]{12}"
            v-model="telefono"
            required
          />
          <span class="block text-sm text-center text-white pt-3 mt-10 mb-14"
            >Si es tu primera vez tendras 14 dias gratis de premium</span
          >
        </form>
        <button
          v-if="ProceedToContinue"
          class="mx-auto mb-10 block bg-blue-green text-white rounded-sm shadow uppercase font-bold text-sm w-52 text-center px-2 py-2"
          style="letter-spacing: 0.25em"
        >
          Continuar
        </button>
        <input
          v-if="ValidatePhone"
          placeholder="Codigo"
          id="code"
          name="code"
          class="block mb-10 uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-11/12 mx-auto py-2"
          pattern="[0-9]{12}"
          v-model="code"
          required
        />
        <button
          v-if="ValidatePhone"
          class="mx-auto block w-52 mb-10 bg-blue-green text-white rounded-sm shadow uppercase font-bold text-sm text-center px-16 py-2"
          style="letter-spacing: 0.25em"
          @click="validated()"
        >
          Validar
        </button>
        <button
          v-if="ValidatePhone"
          class="mx-auto block w-52 mb-10 text-blue-green bg-white rounded-sm shadow uppercase font-bold text-sm text-center px-1 py-2"
          style="letter-spacing: 0.25em"
          @click="cambiarTelefono"
        >
          Cambiar Telefono
        </button>
        <!-- Cambia tu teléfono Area -->
        <div class="mb-10" v-if="CambiaTelefonoElements">
          <span
            class="leading-relaxed uppercase font-bold lg:text-4xl text-3xl mb-1 block lg:whitespace-nowrap"
            >Cambia tu teléfono</span
          >
          <span class="uppercase lg:text-2xl text-xl font-light"
            >Lo usamos para validar tu teléfono</span
          >
          <span class="uppercase border-2 border-white mt-2 block w-24"></span>
        </div>
        <input
          v-if="CambiaTelefonoElements"
          placeholder="Telefono"
          id="cambia_telefono"
          name="cambia_telefono"
          class="block mt-20 mb-10 uppercase rounded-sm text-xs text-center text-dark-gray text-wide bg-white lg:w-80 w-11/12 mx-auto py-2"
          pattern="[0-9]{12}"
          v-model="cambia_telefono"
          required
        />
        <button
          v-if="CambiaTelefonoElements"
          class="mx-auto block w-52 mb-10 bg-blue-green text-white rounded-sm shadow uppercase font-bold text-sm text-center px-2 py-2"
          style="letter-spacing: 0.25em"
        >
          Cambiar
        </button>
        <!-- for Cambia tu teléfono Elements -->
        <div class="mx-auto w-min lg:flex" v-if="RegisterForm">
          <button
            class="font-bold text-base text-center letter-spacing-0-25-em uppercase text-blue-green bg-white rounded-sm w-52 py-1.5 whitespace-nowrap lg:mr-10 mx-auto shadow-md lg:mt-0 lg:mb-0 mt-5 mb-5"
            @click="register()"
          >
            REGISTRARME
          </button>
          <button
            class="whitespace-nowrap font-bold text-base py-1.5 text-center letter-spacing-0-25-em text-white bg-blue-green shadow-md w-52 lg:mx-0 mx-auto"
            @click="registerIni()"
          >
            YA TENGO CUENTA
          </button>
        </div>
        <AlertaErrors :error="error" v-if="error !== null" @CloseError="error = null" />
      </div>
    </div>
  </div>
</template>



<style lang="scss" scoped>
option {
  line-height: 15px !important;
  letter-spacing: 0.25em !important;
  border-bottom: 1px solid #000000;
  height: 40px !important;
  padding: 10px 0 !important;
  color: #3c3c3b;
}
.alert-icon {
  background: url("~/static/img/icon/alert_icon.png");
  width: 32px;
  height: 30px;
}
select {
  background: url("~/static/img/icon/chevron-down.png") no-repeat right #ffffff;
  -webkit-appearance: none;
  background-position-x: 98%;
}
.text-dark-gray {
  color: #3c3c3b;
}
select:required:invalid {
  color: #adb2ba;
}
option[value=""][disabled] {
  display: none;
}
.bg-gradient {
  background: linear-gradient(
    163.41deg,
    rgba(28, 73, 107, 0.9) 0%,
    rgba(0, 169, 157, 0.9) 100%
  );
}
.close-btn {
  background-image: url("~/static/img/icon/close_icon.png");
  width: 35px;
  height: 28px;
}
.w-800 {
  width: 800px;
}
.h-800 {
  height: 800px;
}
.text-blue-green {
  color: #00a99d;
}
.h-474 {
  height: 474px;
}
.letter-spacing-0-25-em {
  letter-spacing: 0.25em;
}
.bg-blue-green {
  background: #00a99d;
}
.bg-gray {
  background: #e2e2e2;
}
.h-474 {
  height: 474px;
}
.letter-spacing-0-25-em {
  letter-spacing: 0.25em;
}
.border-red {
  border-color: #c8142e;
}
.text-red {
  color: #c8142e;
}
.bg-red {
  background: #c8142e;
}
@media only screen and (max-width: 1023px) {
  .w-800 {
    width: auto;
  }
}
</style>
