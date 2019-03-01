<template>
    <section>
        <!-- transition 태그는 목록에 애니메이션을 추가할 때 사용되는 태그이며, tag 속성에 애니메이션이 들어갈 HTML 태그를 지정한다. name 속성은 CSS 클래스와 연관있다. -->
        <transition-group name="list" tag="ul">
            <!-- v-for 디렉티브로 반복한 요소는 모두 뷰에서 내부적으로 인덱스를 부여한다. -->
            <!-- <li v-for="(todoItem, index) in todoItems" class="shadow"> -->
            <li v-for="(todoItem, index) in propsdata" v-bind:key="todoItem" class="shadow"> <!-- App.vue 컴포넌트에서 전달받은 propsdata의 데이터를 꺼낸다. -->
                <i class="checkBtn fas fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                <span class="removeBtn" type="button" @click="removeTodo(todoItem, index)"> <!-- @click은 v-on:click 과 동일하게 작동한다 -->
                    <i class="far fa-trash-alt" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>

<script>
export default {
    props : [
        'propsdata'
    ],
    /* 이 블록의 코드는 App.vue 컴포넌트로 이동되었다.
    data() {
        return {
            todoItems : []
        }
    },
    */
    /* 이 블록의 코드는 App.vue 컴포넌트로 이동되었다.
    created() { // 뷰 인스턴스가 생성되자마자 뷰 데이터에 접근할 수 있도록 created 라이프 사이클 훅에서 로컬 스토리지의 데이터를 뷰 데이터로 옮긴다.
        if (localStorage.length > 0)
        {
            // 로컬 스토리지는 저장된 아이템들을 한번에 불러오는 API가 없으므로 for문으로 아이템을 불러와야한다.
            for (let i = 0; i < localStorage.length; i += 1)
            {
                this.todoItems.push(localStorage.key(i))
            }
        }
    },
    */
    data() {
        return {
            showModal : false
        }
    },
    methods : {
        removeTodo(todoItem, index) {
            // localStorage.removeItem(todoItem)
            // this.todoItems.splice(index, 1) // splice는 자바스크립트에 내장된 API이다.
            // 이벤트 전달 방식으로 변경
            this.$emit('removeTodo', todoItem, index) // 하위 컴포넌트에서 이벤트를 발생시켜 상위 컴포넌트로 신호를 보낼 때 $emit을 사용한다.
        }
    }
}
</script>

<style>
    ul {
        list-style-type : none;
        padding-left : 0px;
        margin-top : 0;
        text-align : left;
    }
    li {
        display : flex; /* 비율 기준의 레이아웃 방식인 flex로 지정 */
        min-height : 50px;
        height : 50px;
        line-height : 50px;
        margin : 0.5rem 0;
        padding : 0 0.9rem;
        background : white;
        border-radius : 5px;
    }
    .checkBtn {
        line-height : 45px;
        color : #62ACDE;
        margin-right : 5px;
    }
    .removeBtn {
        margin-left : auto;
        color : #DE4343;
    }
    /* 데이터가 들어오고 나가는 동작에 대한 효과 */
    /* https://vuejs.org/v2/guide/transitions, https://vuejs.org/v2/guide/transtion-Classes 참고 */
    .list-enter-active, .list-leave-active { 
        transition : all 1s;
    }
    .list-enter, .list-leave-to { 
        opacity : 0;
        transform : translateY(30px);
    }
</style>