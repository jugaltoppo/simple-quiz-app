<template>

    <div>
        <h1>score: {{correctAnswer}}/{{attemptedQuestion}}</h1>
        <button>Reset</button>
    </div>

</template>

<script>
export default {
    props: ['correctAnswer','attemptedQuestion']
}
</script>