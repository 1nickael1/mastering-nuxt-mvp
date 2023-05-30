<template>
    <div>
        <NuxtLink to="/">Voltar</NuxtLink>
        <p v-if="pending">Carregando</p>
        <div v-if="!pending && resultadoUrl?.type == 'pagina'">
            <p>Componente da pagina de produto</p>
            <p>Conteudo da página: {{ JSON.stringify(resultadoUrl.content) }}</p>
        </div>
        <div v-if="!pending && resultadoUrl?.type == 'categoria'">
            <p>Componente da pagina de categoria</p>
            <p>Conteudo da categoria: {{ JSON.stringify(resultadoUrl.content) }}</p>
        </div>

        <p v-if="error">404 not found</p>
    </div>
</template>
<script setup lang="ts">

onMounted(() => {
    // console.log('mount')
})

const { pending, error, data: resultadoUrl } = await useAsyncData('teste', () => makeRequest())

async function makeRequest() {
    const paginas = ['/teste1', '/teste2'];
    const categorias = ['/teste3', '/teste4'];
    const route = useRoute();
    const checarTipoDePagina = new Promise<'pagina' | 'categoria'>((resolve, reject) => {
        setTimeout(() => {
            if (paginas.includes(route.fullPath)) {
                resolve('pagina');
                return;
            }

            if (categorias.includes(route.fullPath)) {
                resolve('categoria');
                return;
            }

            reject(new Error('Erro'))
        }, 1000);
    })

    const tipoDaPagina = await checarTipoDePagina;

    type paginaProduto = {
        type: string;
        content: contentProduto
    }

    type contentProduto = {
        title: string;
    }

    type paginaCategoria = {
        type: string;
        content: contentCategoria
    }

    type contentCategoria = {
        title: string;
        sku: string;
    }

    let resolvePromise;

    if (tipoDaPagina == 'pagina') {
        resolvePromise = new Promise<paginaProduto>((resolve, reject) => {
            setTimeout(() => {
                resolve({
                    type: tipoDaPagina,
                    content: {
                        title: 'Titulo da pagina aleatoria'
                    }
                })
            }, 2000);
        })
    }

    if (tipoDaPagina == 'categoria') {
        resolvePromise = new Promise<paginaCategoria>((resolve, reject) => {
            setTimeout(() => {
                resolve({
                    type: tipoDaPagina,
                    content: {
                        title: 'Titulo da categoria aleatoria',
                        sku: 'Sku aleatorio'
                    }
                })
            }, 1000);
        })
    }

    return resolvePromise
}

</script>