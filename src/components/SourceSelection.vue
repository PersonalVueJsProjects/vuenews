<template>
    <div class="sourceselection">
        <div class="jumbotron">
        <h2><span class="glyphicon glyphicon-list"></span> News List</h2>
        <h4>Select News Source</h4>
        <select class="form-control select-css" @change="sourceChanged">
            <option value="">--- Choose your News source ---</option>
            <option v-bind:value="source.id" v-for="source in sources" :key="source.id">{{source.name}}</option>
        </select>
        <div v-if="source" class="desc">
            <h6 >{{source.description}}</h6>
            <a v-bind:href="source.url" class="btn btn-primary" target="_blank">Go To {{source.name}} Website</a>
        </div>
        <div v-else class="desc">
            <h6>Vuenews.com is your Source for Aggregated News</h6>
        </div>
        </div>
        
        </div>
</template>


<script>

export default {
    name: 'SourceSelection',
    data () {
      return {
        sources: [],
        source: '',
      }  
    },
    methods: {
        sourceChanged (event) {
            for (var i = 0; i < this.sources.length; i++){
                if (this.sources[i].id == event.target.value){
                  this.source = this.sources[i];
                    this.$emit('sourceChanged', event.target.value); 

                }
            }
    }
},
    created : function () {
        this.$http.get('https://newsapi.org/v2/sources?&language=en&apiKey=cf0866b5aaef42e995f9db37bb3f7ef4')
        .then(response => {
           this.sources = response.data.sources; 
        })
        .catch(error => console.log(error));
    }
}


</script>



<style>
.select-css {
	display: block;
	font-size: 16px;
	font-family: sans-serif;
	font-weight: 700;
	color: #444;
	line-height: 1.3;
	padding: .6em 1.4em .5em .8em;
	width: 100%;
	max-width: 100%;
	box-sizing: border-box;
	margin: 0;
	border: 1px solid #aaa;
	box-shadow: 0 1px 0 1px rgba(0,0,0,.04);
	border-radius: .5em;
	-moz-appearance: none;
	-webkit-appearance: none;
	appearance: none;
	background-color: #fff;
	background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23007CB2%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E'),
	  linear-gradient(to bottom, #ffffff 0%,#e5e5e5 100%);
	background-repeat: no-repeat, repeat;
	background-position: right .7em top 50%, 0 0;
	background-size: .65em auto, 100%;
}
.select-css::-ms-expand {
	display: none;
}
.select-css:hover {
	border-color: #888;
}
.select-css:focus {
	border-color: #aaa;
	box-shadow: 0 0 1px 3px rgba(59, 153, 252, .7);
	box-shadow: 0 0 0 3px -moz-mac-focusring;
	color: #222;
	outline: none;
}
.select-css option {
	font-weight:normal;
}

/* Support for rtl text, explicit support for Arabic and Hebrew */
*[dir="rtl"] .select-css, :root:lang(ar) .select-css, :root:lang(iw) .select-css {
	background-position: left .7em top 50%, 0 0;
	padding: .6em .8em .5em 1.4em;
}

/* Disabled styles */

.select-css:disabled:hover, .select-css[aria-disabled=true] {
	border-color: #aaa;
}

.desc {
    margin-top: .6rem;
}
</style>