<script lang="ts" setup>
import UploadProductPic from "./UploadProductPic.vue"
import SelectProductCategory from "./SelectProductCategory.vue"
import BasicInformation from "./BasicInformation.vue"
import SalesInformation from "./SalesInformation.vue"
import ServiceCommitment from "./ServiceCommitment.vue"
import LogisticsInformation from "./LogisticsInformation.vue"
import DetailInformation from "./DetailInformation.vue"

defineProps({
    product: {
        type: Object,
        required: true
    }
})

</script>

<template>
    <SelectProductCategory />
    <!-- Up is down -->
    <UploadProductPic />
    <BasicInformation />
    <SalesInformation />
    <ServiceCommitment />
    <LogisticsInformation />
    <DetailInformation />
</template>