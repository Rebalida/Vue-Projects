<template>
    
    <header>
        <nav class="container">
            <RouterLink to="/">
                <div class="branding">
                <img src="../assets/vue-logo.png" alt="">
                <h1>
                    Projects
                </h1>
            </div>
            </RouterLink>
        </nav>
    </header>

</template>

<script setup>
    import { RouterLink } from 'vue-router';
</script>

<style lang="scss" scoped>
    header{
        background-color: #1c1c1c;

        nav{
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 25px 15px;
            
            .branding{
                display: flex;
                align-items: center;
                gap: 8px;
                img{
                    max-width: 70px;
                }
                h1{
                    color: #f0f0f0;
                    font-size: 24px;
                }
            }

            a {
                text-decoration: none;
                color: inherit;
            }
        }
    }
</style>