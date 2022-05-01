<template>
    <div>
        <!-- THERE SHOULD BE INPUT COMPONENT-->
        <form>
            <input 
                class="input"
                type="text" 
                placeholder="Add new task"
                v-model="taskName"
            />
            <button 
                class="btn"
                type="submit" 
                @click="addNewTask"
            >
                Submit
            </button>
        </form>
        <ul>
            <li v-for="item in items" :key="item.index">
                <!-- THERE SHOULD BE ITEM COMPONENT WHICH WOULD BE LOOPED HERE -->
                {{ item }}
            </li>
        </ul>
        <p v-if="items.length >= listLength">List is already {{ listLength }} items long</p>
    </div>
</template>

<script>
export default {
    name: 'ToDoList',
    components: {
        // TaskInput,
        // ListItem,
    },
    data: () => ({
        taskName: '',
        items: [],
        listLength: 10,
    }),
    methods: {
        /**
         * Checks if value exists - if yes, then value is added in front, 
         * if not - then index of existing value is found and then this value is moved to the front
         * TODO: for the filter - convert to lowercase, so the same value with different cases would not be added as doublicate
         */
        addNewTask(event) {
            event.preventDefault(); //To prevent page reload

            // To limit the length of the list
            if (this.items.length >= this.listLength) {
                return;
            }
        
            // Logic for value addition
            if (!this.items.includes(this.taskName)) {
                this.items.unshift(this.taskName);
            } else {
                this.filtersExistingValues();
            }
            
            //Clears input
            this.taskName = '';
        },
        /**
         * Adds new value and removes existing value
         * TODO: Clean up this long chain of values
         */
        filtersExistingValues() {
            this.items.unshift(this.items.splice(this.items.indexOf(this.taskName), 1).toString());
        }
    }
}
</script>

<style scoped>
.btn {
    margin-left: 8px;
    padding: 6px;
}
.input {
    padding: 6px;
}
</style>