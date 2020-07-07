<template>
  <div id="app" class="h-screen flex flex-col items-center justify-center text-3xl">
    <div>Application Count: {{applications.length}}</div>
    <div>Business Capability Count: {{businessCapabilities.length}} </div>
    <div>View Mapping Count (Business Capabilities): {{viewData ? viewData.mapping.length : ''}}</div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      applications: [],
      businessCapabilities: [],
      viewData: {}
    }
  },
  async created () {
    await this.$lx.init()
    const config = {
      facets: [
        {
          key: 'firstFacet',
          fixedFactSheetType: 'Application',
          callback: applications => { this.applications = applications }
        },
        {
          key: 'secondFacet',
          fixedFactSheetType: 'BusinessCapability',
          callback: businessCapabilities => { this.businessCapabilities = businessCapabilities }
        }
      ],
      reportViewFactSheetType: 'BusinessCapability',
      reportViewCallback: viewData => { this.viewData = viewData }
    }
    this.$lx.ready(config)
  }
}
</script>
