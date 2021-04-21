<template>
    <div class="container-chat">
        <!--        -->
        <div>
            <a-avatar
                    src="https://pic.netbian.com/uploads/allimg/210413/005834-161824671427be.jpg"
                    style="display: inline-block;border: 1px solid #1890ff; "
                    :size="50"
            />
        </div>
        <div class="">
            <a-avatar
                    src="https://pic.netbian.com/uploads/allimg/210414/230430-161841267033a6.jpg"
                    style="display: inline-block;border: 1px solid #1890ff; "
                    :size="50"
            />
        </div>

    </div>

</template>

<script>
    export default {
        name: "Chat"
    }
</script>

<style scoped>
    .container-chat{
        width: 100%;
        height: 100%;
        overflow: auto;
        border: 1px solid black;
    }

</style>
