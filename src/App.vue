<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Namerator</h1>
      <br>
      <h6 class="text-secondary">Gerador de nome</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">{{prefixes.length}}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefix in prefixes" :key="prefix">
                    <div class="row">
                      <div class="col-md">
                        {{prefix}}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" @click="deletePrefix(prefix)"><span class="fa fa-trash"></span></button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br>
                <div class="input-group">
                  <input type="text" class="form-control" placeholder="Digite o prefixo" @keyup.enter="addPrefix(prefix)" v-model="prefix">
                  <div class="input-group-append">
                    <button class="btn btn-info" @click="addPrefix(prefix)"><span class="fa fa-plus"></span></button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">{{sufixes.length}}</span></h5>
            <div class="card">
              <div class="card-body">
                  <ul class="list-group">
                  <li class="list-group-item" v-for="sufix in sufixes" :key="sufix">
                    <div class="row">
                      <div class="col-md">
                        {{sufix}}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" @click="deleteSufix(sufix)"><span class="fa fa-trash"></span></button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br>
                <div class="input-group">
                  <input type="text" class="form-control" placeholder="Digite o sufixo" @keyup.enter="addSufix(sufix)" v-model="sufix">
                  <div class="input-group-append">
                    <button class="btn btn-info" @click="addSufix(sufix)"><span class="fa fa-plus"></span></button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br>
            <h5>Dominios <span class="badge badge-info">{{domains.length}}</span></h5>
            <div class="card">
              <div class="card-body">
                  <ul class="list-group">
                  <li class="list-group-item" v-for="domain in domains" :key="domain.name">
                    <div class="row">
                      <div class="col-md">
                        {{domain.name}}
                      </div>
                      <div class="col-md text-right">
                        <a class="btn btn-info" :href="domain.checkout" target="_blank">
                          <span class="fa fa-shopping-cart"></span>
                        </a>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css"
import "font-awesome/css/font-awesome.css"

export default {
  name: 'App',
  components: {
  },

  data: function () {
    return {
      prefixes: ['b','a'],
      sufixes: ['c', 'd'],
      prefix: '',
      sufix: ''
    };
  },

  methods: {
    addPrefix(prefix){
      this.prefixes.push(prefix);
      this.prefix = '';
    },
    addSufix(sufix){
      this.sufixes.push(sufix);
      this.sufix = '';
    },
    deletePrefix(prefix){
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
    },
    deleteSufix(sufix){
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
    }
  },

  computed: {
    domains(){
      console.log('oi')
      const domains = [];
      for(const prefix of this.prefixes){
        for(const sufix of this.sufixes){
          const name = prefix+sufix
          const url = name.toLowerCase();
          const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
          domains.push({name, checkout})
        }
      }
      return domains
    },
  }
}
</script>

<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}

#main{
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
