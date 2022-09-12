<template>
    <div class="full-container">
        <div class="main-container">
            <div class="main-title">
                <h1>TODOLIST</h1>
            </div>
            <div class="main-content__bar">
                <input type="text" placeholder="what needs to be done?" v-model="newInput" @keyup.enter="addTodo"/>
                <button @click="addTodo">+</button>
            </div>
            <div class="main-content__list">
                <div class="main-content__list__todo" v-for="(item, index) in todoList" :key="index">
                    <input ref="checkbox" type="checkbox" :disabled="item.status" :checked="item.checked"
                           @change="toggle(item, $event)">
                    <input type="text" v-model="item.name"
                           :class="{'finished': item.checked === true}"
                           :disabled="!item.status" />
                    <button v-if="!item.status" @click="editTodo(item)">
                        <i class="fa-solid fa-pencil"></i>
                    </button>
                    <button v-else @click="saveTodo(item)">
                        <i class="fa-solid fa-check"></i>
                    </button>

                    <button @click="deleteTodo(index)">
                        <i class="fa-solid fa-x"></i>
                    </button>
                </div>
            </div>
            <div class="footer-container">
                <button @click="removeChecked">remove checked</button>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'to-do-list',
    components: {},
    data() {
        return {
            todoList: [],
            newInput: '',
            checkedItems: [],
        }
    },
    mounted() {
        window.detail = this;
    },
    watch: {
        checkedItems: {
            deep: true,
            handler(value) {
                console.log('체크된 아이템 : ', value);
            }
        }

    }
    ,
    methods: {
        addTodo() {
            if (this.newInput.length === 0) return;
            this.todoList.push({name: this.newInput, status: false, checked: false});
            this.newInput = '';
        }
        ,

        deleteTodo(index) {
            this.todoList.splice(index, 1);
        }
        ,
        toggle(item, event) {
            item.checked = event.target.checked;

            const list = this.checkedItems;
            const index = list.indexOf(item);

            if (index > -1) {
                list.splice(index, 1)
            } else {
                list.push(item);
            }

        }
        ,
        editTodo(item) {
            item.status = !item.status;
        }
        ,

        saveTodo(item) {
            if(item.name.length < 1) {
                alert('내용이 없습니다');
            } else {
                item.status = !item.status;
            }
        }
        ,

        removeChecked() {
            const todos = this.todoList;
            const checks = this.checkedItems;

            if (checks.length < 1) {
                alert('삭제할 todo를 선택해주세요');
            }

            for (let i = 0; i < checks.length; i++) {
                const condition = todos.includes(checks[i]); // return true or false
                const targetIndex = todos.indexOf(checks[i]);
                if (condition) {
                    todos.splice(targetIndex, 1);
                }
            }
            this.checkedItems = [];
        },


    }
}
</script>

<style>
body {
    background-color: #5E9ABE;
}

.full-container {
    display: flex;
    justify-content: center;

}

.main-container {
    background-color: white;
    display: flex;
    align-items: center;
    flex-direction: column;
    width: 80%;
    margin-top: 30px;
}

.main-content__bar {
    width: 70%;
    padding-bottom: 30px;
    margin-left: 30px;
}

.main-content__bar input {
    height: 30px;
    width: 80%;
    text-align: center;
    border-color: #5E9ABE;
    /*border: none;*/
    border-radius: 5px;
}

.main-content__bar button {
    margin-left: 10px;
    height: 35px;
    width: 35px;
    background-color: #5E9ABE;
    color: white;
    border: none;
    border-radius: 5px;

}

.main-content__bar button:hover {
    cursor: pointer;
}

.finished {
    text-decoration: line-through;
}

.main-content__list {
    margin-bottom: 30px;
    display: flex;
    flex-direction: column;
    width: 80%;
}

.main-content__list__todo {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    justify-content: space-between;
    height: auto;
}

input[type="checkbox"] {
    width: 25px;
    height: 25px;
}

input[type="text"] {
    height: 30px;
    width: 70%;
}

.main-content__list__todo button {
    height: 30px;
    width: 30px;
}

.footer-container {
    margin-bottom: 30px;
    display: flex;
    width: inherit;
    justify-content: right;
}

.footer-container button {
    height: 30px;

}


</style>
