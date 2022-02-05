<template>
    <Layout>
        <h1 v-html="$page.customer.name" />
        <div v-html="$page.customer.position" />
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
