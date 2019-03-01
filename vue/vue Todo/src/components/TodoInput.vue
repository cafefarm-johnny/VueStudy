<template>
    <div class = "inputBox shadow">
        <input type = "text" v-model="newTodoItem" placeholder = "Todo 항목을 작성해주세요." v-on:keyup.enter = "addTodo"> <!-- 인풋 박스에서 엔터를 입력하면 저장하도록 이벤트를 캐치 -->
        <span class = "addContainer" v-on:click = "addTodo">
            <i class = "addBtn fas fa-plus" aria-hidden = "true"></i> <!-- 어썸 Style 적용 -->
        </span>

        <modal v-if="showModal" @close="showModal=false">
            <h3 slot="header">경고</h3> <!-- modal 헤더 -->
            <span slot="body">할 일을 입력하세요.</span> <!-- modal 바디 -->
            <span slot="footer" @click="showModal=false"> <!-- modal 푸터 -->
                <button class="closeModalBtn">닫기</button>
            </span>
        </modal>
    </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
    data() {
        return {
            newTodoItem: '',
            showModal : false // 모달 동작을 위한 플래그 값
        }
    },
    methods : {
        // 디자인 패턴 - 단일 책임 원칙
        // 함수 하나가 하나의 기능만을 담당하도록 설계하는 객체 지향 프로그래밍 디자인 패턴 기법
        addTodo() {
            if (this.newTodoItem !== '')
            {
                // 컴포넌트 내에서의 this는 컴포넌트를 가리킨다.
                let value = this.newTodoItem && this.newTodoItem.trim()
                // localStorage.setItem(value, value)
                this.$emit('addTodo', value) // App.vue로 이벤트를 전달할 때 value 객체를 인자로 전달한다.
                this.clearInput();
            }
            else
            {
                this.showModal = !this.showModal // 텍스트 미 입력 시 모달 표현
            }
        },
        clearInput() {
            this.newTodoItem = ''
        }
    },
    components : {
        Modal : Modal // 모달 컴포넌트 등록
    }
}
</script>

<style scoped>
    input:focus {
        outline : none;
    }
    .inputBox {
        background : white;
        height : 50px;
        line-height: 50px;
        border-radius : 5px;
    }
    .inputBox input {
        border-style : none;
        font-size : 0.9rem;
    }
    .addContainer {
        float : right;
        background : linear-gradient(to right, #6478FB, #8763FB);
        display : block;
        width : 3rem;
        border-radius : 0 5px 5px 0;
    }
    .addBtn {
        color : white;
        vertical-align : middle;
    }
    .closeModalBtn {
        background : #42b983;
        height : 40px;
        width : 100px;
        color : white;
        border : none;
        border-radius : 5px;
    }
</style>