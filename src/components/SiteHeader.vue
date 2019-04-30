<template>
    <div>
        <header>
            <a href="#"><h1>My Photography Site</h1></a> 
            
            <div class="menu">
                <ul>
                    <li><a href="#">Home</a></li>
                    <li><a href="#">About</a></li>
                    <li><a href="#">Contact</a></li>
                    <li><a href="#">Blog</a></li>
                    <li><a href="#">Twitter</a></li>
                </ul>
            </div>
        </header>
        <h2 class="text-centered">Hi. I'm a Photographer</h2>
        <p class="text-centered">Add a catchy tagline or description here if you wish.</p>
    </div>
</template>

<script>
export default {
  name: 'SiteHeader'
}
</script>

<style lang="scss">
    header {
        margin:1em 0 0 0;
    }
    header::after{
        content: "";
        clear: both;
        display: table;
    }
    h1 {
        width: 190px;
        height: 72px;
        background: url("../assets/logo.png") top right;
        text-indent: -9999px;
        margin: 0 auto;
    }    
    .menu ul {
        margin:1em 0 0 0;
        padding:0;
    }
    .menu li {
        width:100%;
        padding:0.25em;
        display:block;
        list-style:none;
        margin:0;
        text-align:center;
    }
    .menu li a {
        color:#777;
        text-decoration:none;
        text-transform:uppercase;
    }
    h2 {
        margin:2em auto 1em auto;
    }
    p.text-centered {
        color:#777;
        margin-bottom:3em;
    }

    @media only screen and (min-width: 1024px) {
        h1 {
            margin:0;
            float:left;
        }
        .menu {
            float:right;
        }
        .menu li {
            display:inline;
        }
    }
</style>