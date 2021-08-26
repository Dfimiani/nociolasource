<section class="menu">
    <div class="contenedor" id="platillos">
        <div class="contenedor-menu">
            <div class="contenedor-menu2">
                <h3 class="titulo">Lista de precios</h3>
                <article>
                    {#each productos as producto}
                        <div class="platillo">
                            <p class="nombre">{producto[1]}</p>
                            <p class="precio">${producto[3]}</p>
                            <p class="descripcion">{producto[2]}</p>
                        </div>
                    {/each}
                </article>
            </div>
        </div>
    </div>
</section>

<script>
    import { onMount } from "svelte";
	import axios from "axios";
	import Papa from "papaparse";
    
    $: productos = [];

    async function fetchPrecios(){
        productos = [];
        const res  = await axios.get('https://docs.google.com/spreadsheets/d/e/2PACX-1vQgJVsslhezp_q0HZcM6JcqDa1oy1uCGLB3_tofXcJbHqMXGho4pQTeIzo2EdxYYgfUN22L-Ahk_hwO/pub?gid=0&single=true&output=csv');
        
        productos = Papa.parse(res.data).data;
        
        setTimeout(fetchPrecios,300000);
    }
	onMount(async () => {
        fetchPrecios(); 
	});

</script>

<style>
    .menu {
        width: 800px;
        margin: auto;
    }
    .menu .titulo{
        font-size: 40px;
        font-weight: 300px;
        text-align: center;
    }
    .menu .contenedor-menu{
        box-shadow: 2px 2px 2px gray;
    }
    .menu .contenedor-menu,
    .menu .contenedor-menu2{
        background: #fefefe;
        border: 3px solid #000;
        border-radius: 10px;
        padding: 10px;
        overflow: hidden;
    }

    .menu .contenedor-menu2{
        padding: 40px;
    }
    .menu .platillo{
        margin-bottom: 30px;
        padding-bottom: 20px;
        border-bottom:  4px dotted;
        overflow: hidden;
    }

    .menu .platillo .nombre {        
        font-size: 20px;
        margin-bottom: 15px;
        float: left; 
        font-weight:bold;
    }

    .menu .precio{
        font-size: 20px;
        margin-bottom: 15px;
        float: right;    
        font-weight:bold;
        color: orange;
    }

    .menu .descripcion{
        font-size: 16px;
        color: #676767;
        clear: both;
        float: left;    
    }

    @media (max-width: 640px) {
        .menu {
            width: 100%;
        }
        
        .menu .contenedor-menu2 {
            padding: 20px;
        }

        .menu article p{
            font-size: 16px !important;
            margin-top: 5px;
            margin-bottom: 5px;
        }
        .menu article .platillo {
            display: flex;
            flex-wrap: wrap;
            flex-direction: row;
            align-items: center;
            justify-content: space-between;
        }
    
        .menu article .descripcion {
            justify-self: self-start;
            text-align: left;
            width: 100%;
        }
    }
</style>