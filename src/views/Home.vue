<template>
    <main>

        <div class="container">
            <div class="row">

                <div class="col-4">
                    <RouterLink to="/todo">
                        <div class="card">
                            <div class="card-body">
                                <h5>Todo List</h5>
                            </div>
                        </div>
                    </RouterLink>
                </div>

                <div class="col-4">
                    <RouterLink to="/tracker">
                        <div class="card">
                            <div class="card-body">
                                <h5>Expense Tracker</h5>
                            </div>
                        </div>
                    </RouterLink>
                </div>
                
            </div>
        </div>
    </main>
</template>

<script setup>

</script>

<style lang="scss" scoped>
    h1{
        text-align: center;
    }

    main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 40px 15px;
    font-size: 18px;
    }

    a{
        text-align: center;
        text-decoration: none;
    }
</style>