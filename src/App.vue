<template>
 
<div class="wrapper">
	
    <div class="wrapper-content">

     	<section>
			<div class="container">
				<message  v-if="message" :message="message"> </message> 
                <!-- второй message - это то, что я передаю от родителя в компоненты -->

                <newNote :note="note" @add="addNote"/> 

                <div class="note-header">
                    <h1> {{title}} </h1>

                    <search :value="search" @search="searchAdd($event)" />  
                    <!-- value - это имя prop в компоненте search-->
                    

                    <div class="icons">

                        <svg :class="{active: grid}" @click="grid=true" style="cursor:pointer;" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" ><rect x="3" y="3" width="7" height="7"></rect><rect x="14" y="3" width="7" height="7"></rect><rect x="14" y="14" width="7" height="7"></rect><rect x="3" y="14" width="7" height="7"></rect>
                        </svg>

                        <svg :class="{active: !grid}" @click="grid=false" style="cursor:pointer;"  xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="8" y1="6" x2="21" y2="6"></line><line x1="8" y1="12" x2="21" y2="12"></line><line x1="8" y1="18" x2="21" y2="18"></line><line x1="3" y1="6" x2="3" y2="6"></line><line x1="3" y1="12" x2="3" y2="12"></line><line x1="3" y1="18" x2="3" y2="18"></line>
                        </svg>

                    </div>
                </div>
                

                <notes :notes="notesFilter" @remove="removeNote" :grid="grid" />
				
			</div>
		</section>

        
    </div>
	
</div>
      
</template>





<script>
	import message from '@/components/Message.vue'
    import newNote from '@/components/NewNote.vue'
    import notes from '@/components/Notes.vue'
    import search from '@/components/Search.vue'

	export default {

		components: {
			message: message,
            newNote: newNote, // так как ключ и значение совпадают, то можно оставить только значение
            notes,
            search
		},

		data () {
			return {
				title: 'notes App',

                search: '',

                arr: [],

                message: null,

                grid: true,

                note: {
                    title: '',
                    descr: ''
                },

                notes: [
                    {
                        title: 'The first Note',
                        descr: 'Description for the first note',
                        date: new Date(Date.now()).toLocaleString()
                    },
                    {
                        title: 'The second Note',
                        descr: 'Description for the second note',
                        date: new Date(Date.now()).toLocaleString()
                    },
                    {
                        title: 'The third Note',
                        descr: 'Description for the third note',
                        date: new Date(Date.now()).toLocaleString()
                    }

                ]
			}

			
		},

        computed: {

            notesFilter() {

                let array = this.notes,
                    search = this.search;

                if (!search) { return array};

                search = search.trim().toLowerCase();
                
                array = array.filter(function (item) {

                    if (item.title.toLowerCase().indexOf(search) !== -1) {
                        return item;
                    } 

                }) 
                
                return array;       
            }
        },


            



		methods: {
            addNote () {
                // console.log(this.note)

                if (this.note.title === '') {
                    this.message = 'Error: "Title" can`t be blank!';
                    return false; // можно написать просто return
                };
                

                this.notes.push ( 
                    {
                        title: this.note.title,
                        descr: this.note.descr,
                        date: new Date(Date.now()).toLocaleString()
                    } 
                );

                this.message = null;
                this.note.title = '';
                this.note.descr = '';
            },

            removeNote(i) {
                this.notes.splice(i, 1);                                           
            }, 

            searchAdd(value) {
                // debugger
                this.search = value;
                console.log(this.search)
            }

        }
	
	}

</script>


