<template>
    <div class="new-note">
        <label> Title </label>
        <input type="text" v-model="note.title"> 
        <label> Description </label>
        <textarea v-model="note.descr"> </textarea>
        <button class="btn btnPrimary"  @click = "btnClick"> New note </button>
    </div>
</template>
 

<script>

    export default {

        props: {
            note: {
                type: Object,
                required: true,
            }
        },

        methods: {
            btnClick () {
                this.$emit('add', this.note)
            }
        }
    }

</script>

<style lang="scss" scoped>

    .new-note {
        text-align: center;
    }

    button {
        transition: all  0.4s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        &:hover {
            transform:  translate(0, -6px) ;
            // color: rgb(37, 23, 240);
            box-shadow: 0 30px 30px rgba($color: #000000, $alpha: .4);

        }
    }

    input {
        background-color: rgba(231, 225, 225, 0.897);
    }

    textarea {
         background-color: rgb(231, 225, 225);
    }

</style>