<template>
  <v-card
    class="mx-auto"
    max-width="1000"
  >
    <v-container fluid>
      <v-alert
        v-show="err"
        border="top"
        color="red lighten-2"
        dark
      >
        {{ err }}
      </v-alert>
      <v-row dense>
        <v-col>
          <v-card
            class="mx-auto my-12"
            elevation="0"
            tile
          >
            <v-card-text>
              <v-row
                align="center"
                class="mx-0"
              >
                {{ stdout }}
              </v-row>
            </v-card-text>

            <v-divider class="mx-4" />
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
import { exec } from 'child_process'

export default {
  name: 'ShellExec',
  components: {},
  data () {
    return {
      err: '',
      stdout: '',
      stderr: ''
    }
  },
  created () {
    exec('docker container ls -a', (err, stdout) => {
      if (err) {
        this.err = err
      } else {
        for (const line of stdout) {
          this.stdout += line
        }
      }
    })
  }
}
</script>
