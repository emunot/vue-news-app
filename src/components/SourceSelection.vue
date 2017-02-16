<template>
    <div class="sourceselection">
        <div>
            <div class="jumbotron">
                <h2><span class="glyphicon glyphicon-list-alt"></span>&nbsp;News Around the World</h2>
                <h6>Select News Source</h6>
                <div class="col-md-4 float-left"></div>
                <select class="form-control col-md-4" v-on:change="sourceChanged">
                    <option selected disabled value="">Please select news source ...</option>
                    <option v-for="source in sources" v-bind:value="source.id">{{source.name}}</option>
                </select>
                <div class="col-md-4"></div>
                <div v-if="source">
                    <p class="small">{{source.description}}</p>
                    <a v-bind:href="source.url" class="btn btn-primary" target=_blank>Go to {{source.name}} Website</a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'sourceselection',

        data () {
            return {
                sources: [],
                source: ''
            }
        },

        methods: {
            sourceChanged: function(e) {
                for (var i=0; i<this.sources.length; i++){
                    if (this.sources[i].id == e.target.value) {
                        this.source = this.sources[i];
                    }
                }
                this.$emit('sourceChanged', e.target.value);
            }
        },

        created: function () {
            this.$http.get('https://newsapi.org/v1/sources?language=en')
            .then(response => {
                this.sources = response.data.sources;
            });
        }
    }
</script>

<!-- Add "scoped" attribute to limit css to this component only -->
<style scoped>

</style>