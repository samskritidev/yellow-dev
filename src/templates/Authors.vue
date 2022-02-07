<template>
    <Layout>
        <h1 v-html="$page.author.name" />
        <div v-html="$page.author.position" />
    </Layout>
</template>

<page-query>
    query Author($id: ID!) {
    author(id: $id) {
    name
    position
    }
    }
</page-query>
