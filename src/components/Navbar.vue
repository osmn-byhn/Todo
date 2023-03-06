<script setup>
    const toggle = () => {
        var icon = document.getElementById('icon')
        if(document.body.classList.contains("light")){
            document.body.classList.remove("light")
            icon.setAttribute('class', 'bi bi-sun-fill')
        } else {
            document.body.classList.add("light")
            icon.setAttribute('class', 'bi bi-moon-fill')
        }
    }
</script>

<template>
    <nav>
        <ul>
            <li>
                <h1>Notes</h1>
            </li>
            <li>
                <i class="bi bi-sun-fill" id="icon" @click="toggle()"></i>
            </li>
        </ul>
    </nav>
</template>

<style scoped lang="scss">
    @import '../../public/Navbar.scss'
</style>