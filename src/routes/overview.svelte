<script context="module">
    export async function preload({ params }, { token }){
        if (!token){
            this.redirect(302, "/login");
        }
    }
</script>
<script>
    import {post} from "utils.js";
    async function getMyData(){
        return await post(`auth/getMyData`);
    }
</script>
{#if process.browser}
    {#await getMyData()}
        Loading...
    {:then my}
        <section>
            <p>{my.name}</p>
        </section>
        <section>
            My funds
            <p>{my.funds}</p>
        </section>
        <pre>{JSON.stringify(my, null, 4)}</pre>
    {/await}
{/if}