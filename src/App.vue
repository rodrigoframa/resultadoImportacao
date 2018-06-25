<template>
  <div id="app">
    <div class="col-lg-12">
      <button class="btn btn-primary" @click="processaResposta">Trazer resposta</button>
      <div class="ibox">
          <div class="ibox-title">
              <h5>Example of initial collapsed panel</h5>
              <div class="ibox-tools">
                  <a class="collapse-link">
                    <i class="fa fa-chevron-up"></i>
                  </a>
                  <a class="dropdown-toggle" data-toggle="dropdown" href="#">
                    <i class="fa fa-wrench"></i>
                  </a>
                  <ul class="dropdown-menu dropdown-user">
                    <li><a href="#">Config option 1</a></li>
                    <li><a href="#">Config option 2</a></li>
                  </ul>
                  <a class="close-link">
                    <i class="fa fa-times"></i>
                  </a>
              </div>
          </div>
          <div class="ibox-content">
              <p>
                  Aenean commodo ligula eget dolor. Aenean massa. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Donec quam felis, ultricies nec, pellentesque eu, pretium quis, sem. Nulla consequat massa quis enim. </p>
              <p>
                  Donec pede justo, fringilla vel, aliquet nec, vulputate eget, arcu. In enim justo, rhoncus ut, imperdiet a, venenatis vitae, justo. Nullam dictum felis eu pede mollis pretium. Integer tincidunt. Cras dapibus. Vivamus elementum semper nisi.
              </p>
          </div>
          <div class="row"> 2 </div>
          <div class="col-lg-4">
            <div class="panel panel-primary" v-if="resultado.sucesso.length > 0" @click="panel = !panel">
              <div class="panel-heading">
                <strong>{{ resultado.sucesso.length }} Guias importadas com Sucesso </strong> <small>(clique para detalhes)</small>
              </div>
              <div class="panel-body" v-show="panel">
               teste
             </div>
            </div>
          </div>
          <br>
          <hr>
          <div v-for="(status,key) in resultado" :key="key" :class="'panel panel-'+ status.class" v-if="status.guias.length > 0" @click="status.detail = !status.detail">
            <div class="panel-heading">
              <strong>{{ status.guias.length +' - '+ status.descricao }} </strong> <small>(clique para detalhes)</small>
            </div>
            <div class="panel-body" v-show="status.detail">
               <ul class="unstyled">
                 <li :class="'text-'+status.class" v-for="(guia,key) in status.guias" :key="key">
                 {{ guia.cpf + ' - '+ guia.motivo}}
               </li>
               </ul>
            </div>
          </div>
          <div class="row"></div>
          <div class="alert alert-success">
            How quickly daft jumping zebras vex. <a class="alert-link" href="#">Alert Link</a>.
          </div>
          <div class="alert alert-danger">
            How quickly daft jumping zebras vex. <a class="alert-link" href="#">Alert Link</a>.
          </div>
          <div class="alert alert-warning">
            How quickly daft jumping zebras vex. <a class="alert-link" href="#">Alert Link</a>.
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      panel: false, 
      response : [{ cpf:'11111111',  motivo: 'ja foi importado',  resultado: 2 },
      { cpf:'22222222222',  motivo: 'ja foi importado',  resultado: 2 },
      // { cpf:'333333333',  motivo: 'importado com sucesso',  resultado: 1 },
      // { cpf:'444444444',  motivo: 'importado com sucesso',  resultado: 1 },
      // { cpf:'555555555',  motivo: 'importado com sucesso',  resultado: 1 },
      { cpf:'666666666',  motivo: 'cpf invalido',  resultado: 0 },
      { cpf:'777777777',  motivo: 'cpf invalido',  resultado: 0 },
      { cpf:'888888888',  motivo: 'cpf invalido',  resultado: 0 }],
      resultado : {
        erro: {
          class: 'danger',
          descricao: 'Guias com erro!',
          guias: [],
          detail: false
        },
        sucesso: {
          class: 'success',
          descricao: 'Guias importadas com sucesso!',
          guias: [],
          detail: false
        },
        repetido: {
          class: 'warning',
          descricao: 'Guias já foram importadas anteriormente!',
          guias: [],
          detail: false
        }
      }
    }
  },
  methods: { 
    processaResposta () {
      this.response.forEach(obj => {
      if (obj.resultado === 0) {
          // console.log(obj, '0')
          this.resultado.erro.guias = [...this.resultado.erro.guias, {cpf: obj.cpf, motivo: obj.motivo}]
      } else if (obj.resultado === 1 ){
          // console.log(obj,'1')
          this.resultado.sucesso.guias = [...this.resultado.sucesso.guias, {cpf: obj.cpf, motivo: obj.motivo}]
      } else {
          // console.log(obj, '2')
          this.resultado.repetido.guias = [...this.resultado.repetido.guias, {cpf: obj.cpf, motivo: obj.motivo}]
      }
      })
    }
  }
}
</script>

<style>



</style>
