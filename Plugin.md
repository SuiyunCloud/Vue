# Vuex

```js
// in store module, define vuex
const store = new Vuex.Store(
    {
        state:{
            count: 0,
            list: [1,2,5,10,45]
        },
        //mutations can only be used to change the value in vuex, can't async
        mutations:{
            increment(state) {
                state.count ++;
            }
        },
        //getters used to return processed original state variable
        getters: {
            filteredList: state => {
                return state.list.filter(item => item < 10>)
            }
        },

        //function like mutations, but can do async
        actions: {
            increment(state) {
                state.count ++;
            }
        }
    }
)


// in other module
<template>
<div>{{global_count}}</div>
</template>

<script>
export default {
    computed: {
        global_count () {
            return this.$store.state.count  //use $store.state to get data in vuex
        }
    },
    methods: {
        // call mutations' function to change vuex in other module
        handleIncrement (){
            this.$store.commit('increment');
        }
    }
}