<template>
  <q-page class="container" padding>
    <p class="text-h4" style="text-align: center">Formulário</p>
    <div class="row">
      <!-- separar os elementos: class="q-col-gutter-sm" -->
      <q-form
        ref="myForm"
        style="width: 80%; margin: 0 10% 0 10%"
        @submit="onSubmit"
        @reset="onReset"
      >
        <q-input
          outlined
          clearable
          clear-icon="close"
          v-model="form.nome"
          color="indigo-13"
          label="Nome"
          class="col-md-10 col-sm-10 com-xs-10"
          :rules="[(val) => (val && val.length > 0) || 'Digite Seu Nome']"
        >
          <template v-slot:prepend>
            <q-icon name="person" />
          </template>
        </q-input>

        <q-input
          outlined
          v-model="form.dataNascimento"
          color="indigo-13"
          type="date"
          label="Data de Nascimento"
          class="col-md-10 col-sm-10 col-xs-10"
          :rules="[
            (val) => (val && val.length > 0) || 'Coloque a Data de Nascimento',
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="person" />
          </template>
        </q-input>

        <q-option-group
          class="row"
          :options="listaSexo"
          type="radio"
          v-model="form.sexo"
          :rules="[(val) => val || 'Campo Obrigatório']"
        />

        <q-input
          outlined
          clearable
          clear-icon="close"
          v-model="form.email"
          type="email"
          label="Email"
          suffix="@gmail.com"
          class="col-md-10 col-sm-10 col-xs-10"
          :rules="[(val) => (val && val.length > 0) || 'Email Obrigatório']"
        >
          <template v-slot:prepend>
            <q-icon name="mail" />
          </template>
        </q-input>

        <q-input
          outlined
          clearable
          clear-icon="close"
          v-model="form.telefone"
          label="Telefone"
          mask="(##) ### - ######"
          unmasked-value
          class="col-md-10 col-sm-10 col-xs-10"
          :rules="[
            (val) => (val && val.length > 0) || 'Telefone Obrigatório',
            (val) => val.length === 11 || 'Telefone Inválido',
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="phone" />
          </template>
        </q-input>

        <q-input
          outlined
          clearable
          clear-icon="close"
          v-model="form.endereco"
          color="indigo-13"
          label="Endereço"
          class="col-md-10 col-sm-10 com-xs-10"
          :rules="[(val) => (val && val.length > 0) || 'Campo Obrigatório']"
        >
          <template v-slot:prepend>
            <q-icon name="location_on" />
          </template>
        </q-input>

        <div style="max-width: 300px">
          <q-select
            outlined
            clearable
            clear-icon="close"
            v-model="form.uf"
            :options="listaEstados"
            label="UF"
            emit-value
            map-options
            :rules="[(val) => (val && val.length > 0) || 'Campo Obrigatório']"
          >
            <template v-slot:prepend>
              <q-icon name="location_on" />
            </template>
          </q-select>
        </div>

        <!-- dois botões -->
        <div class="col-10">
          <q-btn label="Cadastrar" type="submit" color="primary" />
          <q-btn
            label="Reset"
            type="reset"
            color="primary"
            flat
            class="q-ml-sm"
          />
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
  data() {
    return {
      form: {
        nome: "",
        dataNascimento: null,
        email: "",
        telefone: "",
        uf: "",
        endereco: "",
        sexo: [],
      },
      listaEstados: [
        {
          label: "Pará",
          value: "PA",
        },
        {
          label: "Paraná",
          value: "PR",
        },
        {
          label: "Santa Catarina",
          value: "SC",
        },
        {
          label: "Ceará",
          value: "CE",
        },
      ],
      listaSexo: [
        { label: "Masculino", value: "M" },
        { label: "Feminino", value: "F" },
        { label: "Não Informar", value: "NI" },
      ],
    };
  },

  methods: {
    onSubmit() {
      this.$q.notify({
        message: "Fomulário enviado com Sucesso!",
        color: "positive",
        icon: "check_circle_outline",
      });
      this.onReset();
    },
    async onReset() {
      await this.resetForm();
      this.$refs.myForm.resetValidation();
    },
    async resetForm() {
      this.form = {
        nome: "",
        dataNascimento: null,
        email: "",
        telefone: "",
        uf: "",
        endereco: "",
        sexo: "",
      };
    },
  },
});
</script>
