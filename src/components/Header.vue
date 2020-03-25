<template>

    <div>
        <h1>score: {{correctAnswer}}/{{attemptedQuestion}}</h1>
        <form>
            <button>Reset</button>
        </form>
    </div>

</template>

<script>
export default {
    props: ['correctAnswer','attemptedQuestion']
}
</script>