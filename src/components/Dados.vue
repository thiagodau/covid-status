<template>
  <div class="dados">
    <h1>Dados</h1>
    <div class="dados-body">
      <div class="lista">
        <h1>Status Brasil por Estado (UF)</h1>
        <table>
          <tbody>
            <tr>
              <th>📍 Estado</th>
              <th>🚨 Confirmados</th>
              <th>💀 Mortes</th>
            </tr>
            <tr v-for="dado in dadosEstadosBrasil" :key="dado.id">
              <td>{{ dado.uf }}</td>
              <td>{{ dado.cases }}</td>
              <td>{{ dado.deaths }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div class="card-brasil">
        <h1>Status Geral Brasil</h1>
        <ul>
          <li>✅ {{ dadosBrasil.confirmed }} Confirmados</li>
          <li>📖 {{ dadosBrasil.cases }} Casos</li>
          <li>♻️ {{ dadosBrasil.recovered }} Recuperados</li>
          <li>💀 {{ dadosBrasil.deaths }} Mortes</li>
          <li>Atualizado em: {{ dadosBrasilData }}h</li>
          <li>
            Fonte de Dados:
            <strong
              ><a href="https://covid19-brazil-api.now.sh/"
                >COVID-19 Brazil API</a
              ></strong
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

let BASE_URL = "https://covid19-brazil-api.now.sh/api/report/";

export default {
  data() {
    return {
      dadosEstadosBrasil: "",
      dadosBrasil: "",
      dadosBrasilData: "",
    };
  },
  mounted() {
    this.getDadosEstadosBrasil();
    this.getDadosBrasil();
  },
  methods: {
    getDadosEstadosBrasil() {
      axios
        .get(BASE_URL + "v1")
        .then((response) => {
          this.dadosEstadosBrasil = response.data;
          this.dadosEstadosBrasil = this.dadosEstadosBrasil.data;
        })
        .catch((e) => console.log(e));
    },
    getDadosBrasil() {
      axios
        .get(BASE_URL + "v1/brazil")
        .then((response) => {
          this.dadosBrasil = response.data;
          this.dadosBrasil = this.dadosBrasil.data;

          if (this.dadosBrasil.updated_at) {
            let formatter = Intl.DateTimeFormat("pt-BR", {
              weekday: "long",
              year: "numeric",
              month: "long",
              day: "numeric",
              hour: "numeric",
              minute: "numeric",
            });

            this.dadosBrasilData = formatter.format(
              this.dadosEstadosBrasil.updated_at
            );
          }
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>

<style>
.dados {
  display: block;
  padding: 30px;
}

.dados-body {
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 20px;
}

.lista {
  background: #1a1a1d;
  margin: 0 30px 0 30px;
  padding: 30px;
  border-radius: 30px;
  border: 1px solid #1a1a1d;
}

.lista:hover {
  border: 1px solid #4ffa7b;
}

.lista table {
  width: 100%;
  margin: 10px;
  text-align: center;
}

.card-brasil {
  background: #1a1a1d;
  margin: 0 30px 0 30px;
  padding: 30px;
  border-radius: 30px;
  line-height: 30px;
  border: 1px solid #1a1a1d;
}
.card-brasil:hover {
  border: 1px solid #4ffa7b;
}

.card-brasil ul {
  list-style: none;
  margin: 10px;
}
</style>