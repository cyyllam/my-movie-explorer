<template>
       <b-container class="mt-3">
             <b-card bg-variant="light">
               <b-form-group :label="formlabel">
                   <slot></slot>
                 <p class="mt-3">*Results are from the first page received from tMDB</p>
                 <p>**User rating is out of 10</p>
               </b-form-group>
             </b-card>
        </b-container>
</template>

<script>
export default {
    props: {
        formlabel: String
    }
}
</script>