```Plain
data () {
    return {
        costForm: {
        }
    }
},
watch: {
    costForm: {
      deep: true,
      handler () {
        let disable = this._.includes(this.costForm, null) || this._.includes(this.costForm.someWork, null) ||
          this._.includes(this.costForm.totalParts, null) || this.costForm.invoiceNumber.length < 1 ||
          this.costForm.account.length < 1
        this.$emit('update:submitEnable', !disable)
      }
    }
  }
```