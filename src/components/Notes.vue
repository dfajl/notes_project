<template>
    <div class="notes">
        <div class="note" :class="{full: !grid}" v-for = "(note, index) in notes" :key= "index">

            <div class="note-header" :class="{full: !grid}" >
                <p> {{ note.title }} </p>
                <p class = "close"  @click="removeNote(index)"> x </p>
            </div>

            <div class="note-body">
               <p> {{ note.descr }} </p> 
               <span> {{ note.date }} </span>
            </div>

        </div>
    </div>
</template>



<script>
    export default {

        props: {
                
            notes: {
                type: Array,
                required: true,
            },

            grid: {
                type: Boolean,
                required: true,
            }
        },

        methods: {
            removeNote (ind) {
                console.log(this.notes)
                console.log(`Note id ${ind} removed`);
                this.$emit('remove', ind)
                // debugger
            }
        }      
    } 
</script>

<style lang="scss" >
    
    .notes {
        
        margin-top: 15px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        flex-wrap: wrap;
        padding: 40px 0;
    }

    .note {
        border: 1px solid rgb(238, 216, 216);
        border-radius: 10px;
        width: 48%;
        padding: 18px 20px;
        margin-bottom: 20px;
        background-color: rgb(231, 225, 225);
        transition: all  0.25s cubic-bezier(0.25, 0.46, 0.45, 0.94);
        &:hover {
            box-shadow: 0 30px 30px rgba($color: #000000, $alpha: .4);
            transform: translate(0, -6px);
            transition-delay: 0s !important;
        }

        &.full {
            width: 70%;
            margin: 0 auto;
            margin-bottom: 15px;
            text-align: center;
        }
    }

    .note-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-top: 15px;

        h1 {
            font-size: 32px;
        }

        P {
            margin-bottom: 5px;
            font-size: 22px;
            color: rgb(68, 24, 224)
        }

        svg {
            color: #999;
            margin-right: 12px;

            &:last-child {
                margin-right: 0;
            }

            &.active {
                color: rgb(68, 24, 224)
            }
        }

        .close {
            color:red;
            cursor: pointer; 
    
            &:hover {
                font-weight: 500;
            }
        }

        &.full {
            justify-content: center;
            
            p {
                margin-right: 20px;
            }
            
        }
    }

    .note-body {
        p {
            margin: 20px 0;
        }

        span {
            
            font-size: 14px;
            color: rgb(136, 132, 132);
        }
    }
    

    


</style>