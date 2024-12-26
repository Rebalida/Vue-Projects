<template>
    <main>
        <div class="container">
            <div class="row">

                <div class="col-3">
                    <RouterLink to="/todo" class="button button--pandora">
                        <div class="card project-card">
                            <div class="card-body">
                                <h5>Todo List</h5>
                            </div>
                        </div>
                    </RouterLink>
                </div>

                <div class="col-3">
                    <RouterLink to="/tracker" class="button button--pandora">
                        <div class="card project-card">
                            <div class="card-body">
                                <h5>Expense Tracker</h5>
                            </div>
                        </div>
                    </RouterLink>
                </div>

                <div class="col-3">
                    <RouterLink to="/weather" class="button button--pandora">
                        <div class="card project-card">
                            <div class="card-body">
                                <h5>Weather Report</h5>
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

    .row{
        display: flex;
        flex-flow: wrap row;
        justify-content: center;
    }

    h5{
        margin: 0;
        color: #f0f0f0;
        padding: 5px 0;
    }

    a{
        text-align: center;
        text-decoration: none;
    }

    .button--pandora{
        background: #1c1c1c;
        padding: 0;
        display: block;
    }

    .button--pandora .card{
        background: #2c2c2c;
        border-radius: 0%;
        border: 2px solid #4DBA87;
        transform: translate3d(-4px, -4px, 0);
        transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
        text-align: center;
    }

    .button--pandora:hover .card {
    transform: translate3d(-8px, -8px, 0);
    }

</style>