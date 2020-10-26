<template>
<div style="position:relative" >
    <input class="form-control" type="text" v-model="selection"
        @keydown.enter = 'enter'
        @keydown.down = 'down'
        @keydown.up = 'up'
        @input = 'change'
    />
    <div class="dropdown-menu" style="width:100%;" v-bind:class="{'show':openSuggestion}">
        <a v-for="(suggestion, index) in matches"
            v-bind:class="{'active': isActive(index)}"
            @click="suggestionClick(index)"
            :key="index"
            class="dropdown-item"
            href='#'
        >
            {{ suggestion.name }}
        </a>
    </div>
</div>
</template>
<script>
export default {

    data() {
        return {
            open: false,
            current: 0,
            selection: null,
        }
    },

    props: {
        suggestions: {
            type: Array,
            required: true
        },

        // selection: {
        //     type: String,
        //     required: true,
        // }
    },

    computed: {
        matches() {
            return this.suggestions.filter((str) => {
                return str.name.indexOf(this.selection) >= 0;
            });
        },

        openSuggestion() {
            return this.selection !== "" &&
                   this.matches.length != 0 &&
                   this.open === true;
        }
    },

    methods: {
        enter() {
            this.selection = this.matches[this.current]['name'];
            this.open = false;
        },

        up() {
            if(this.current > 0)
                this.current--;
        },

        down() {
            if(this.current < this.matches.length - 1)
                this.current++;
        },

        isActive(index) {
            return index === this.current;
        },

        change() {
            if (this.open == false) {
                this.open = true;
                this.current = 0;
            }
        },

        suggestionClick(index) {
            this.selection = this.matches[index]['name'];
            this.open = false;
        },
    }
}

</script>
