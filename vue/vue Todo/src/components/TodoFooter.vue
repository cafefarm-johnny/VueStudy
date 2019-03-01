<template>
    <div class="clearAllContainer">
        <span class="clearAllBtn" @click="clearTodo">Clear All</span>
    </div>
</template>

<script>
export default {
    methods : {
        clearTodo() {
            // localStorage.clear()
            // 이벤트 전달 방식으로 변경
            this.$emit('removeAll') // [Clear All] 버튼을 클릭하면 removeAll 이벤트를 발생시켜 App.vue 컴포넌트로 전달한다.
        }
    }
}
</script>

<style>
    .clearAllContainer {
        height : 50px;
        line-height : 50px;
        background-color : white;
        border-radius : 5px;
        margin : 0 auto;
    }
    .clearAllBtn {
        color: #E20303;
        display : black;
    }
</style>