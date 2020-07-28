<template>
  <v-row>
    <v-col>
      <v-row>
        <v-col>
          <v-form
            ref="formUsers"
            v-model="valid"
            @submit.prevent="enviarFormulario"
          >
            <v-container>
              <v-row>
                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="firstname"
                    :rules="nameRules"
                    :counter="10"
                    label="First name"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="lastname"
                    :rules="nameRules"
                    :counter="10"
                    label="Last name"
                    required
                  ></v-text-field>
                </v-col>

                <v-col cols="12" md="4">
                  <v-text-field
                    v-model="email"
                    :rules="emailRules"
                    label="E-mail"
                    required
                  ></v-text-field>
                </v-col>
              </v-row>
              <v-btn type="submit">
                Enviar
              </v-btn>
            </v-container>
          </v-form>
        </v-col>
      </v-row>
      <v-row>
        <v-col>
          <v-list disabled>
            <v-subheader>REPORTS</v-subheader>
            <v-list-item-group v-model="item" color="primary">
              <v-list-item v-for="(item, i) in items" :key="i">
                <v-list-item-content>
                  <v-list-item-title>
                    {{ item.name }} - {{ item.lastname }} - {{item.email}}
                  </v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-col>
      </v-row>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data: () => ({
    item: 1,
    items: [
      {
        name: 'Fabian',
        lastname: 'Salgado',
        email: 'fasalgad@f.cl',
        icon: 'mdi-air-filter'
      },
      {
        name: 'José',
        lastname: 'Veloso',
        email: 'jveloso@f.cl',
        icon: 'mdi-adobe-acrobat'
      },
      {
        name: 'Samuel',
        lastname: 'Salgado',
        email: 'samuel5@f.cl',
        icon: 'mdi-alpha-s'
      }
    ],
    valid: false,
    firstname: '',
    lastname: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => v.length <= 10 || 'Name must be less than 10 characters'
    ],
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+/.test(v) || 'E-mail must be valid'
    ]
  }),
  methods: {
    enviarFormulario () {
      if (this.$refs.formUsers.validate()) {
        alert('formulario correcto')
        this.items.push({
          name: this.firstname,
          lastname: this.lastname,
          email: this.email
        })
      }
    }
  }
}
</script>
