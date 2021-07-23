<template>
    <div>

        <b-modal id="deletePhoneModal" title="Delete Phone" ok-title="Save" @ok="onDelete" ok-variant="danger">
            Are You Sure Want to delete this?
            <br>
            <br>
            <h1>{{phone.phone_name}}</h1>
        </b-modal>

    </div>
</template>

<script>
export default {
    props: {
        phone: {}
    },
    methods: {
        async onDelete() {
            this.$axios.delete('http://localhost:8000/api/phones' + this.phone.id)
            .then((res)=>{
                if(res.status==202) {
                    alert('Phone is deleted Successfully')
                    this.$emit('onDeleted')
                }
            })
        }
    }
    
}
</script>