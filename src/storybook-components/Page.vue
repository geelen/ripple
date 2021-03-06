<template>
  <rpl-base-layout class="demo">
    <template slot="alert">
      <rpl-alert-base v-if="preview">Draft only and not yet published</rpl-alert-base>
      <rpl-alert v-bind="mock.alert" />
    </template>

    <template slot="header">
      <rpl-site-header
        :logo="mock.header.logo"
        :links="mock.header.links"
        :breakpoint="mock.header.breakpoint"
        :searchTerms="mock.header.searchTerms"
        showSearch
        sticky
        @search="searchFunc"
      />
    </template>

    <rpl-page-layout
      :sidebar="sidebar"
      class="main"
      :backgroundGraphic="mock.landingPage.backgroundGraphic"
    >
      <template slot="breadcrumbs">
        <rpl-breadcrumbs :crumbs="mock.breadcrumbs.crumbs" />
      </template>

      <template slot="aboveContent">
        <rpl-hero-banner
          :title="mock.heroBanner.title" :introText="mock.heroBanner.introText"
          :linkHeading="mock.heroBanner.linkHeading" :links="mock.heroBanner.links"
          :moreLink="mock.heroBanner.moreLink"
          :theme="mock.heroBanner.heroBackgroundImage ? 'dark' : 'light'"
          :showLinks="mock.heroBanner.heroBackgroundImage ? false : true"
          class="rpl-site-constrain--on-all"
        />
      </template>

      <template slot="aboveContentTwo">
        <rpl-card-box
          v-bind="mock.cardBox"
          class="rpl-site-constrain--on-all"
        />
        <rpl-search-form
          :title="mock.searchForm.title"
          :searchPlaceholder="mock.searchForm.searchPlaceholder"
          :prefillSearchTerm="mock.searchForm.prefillSearchTerm"
          :theme="mock.searchForm.theme"
          :allowBlank="mock.searchForm.allowBlank"
          class="rpl-site-constrain--on-all"
        />
        <rpl-campaign-primary
          :title="mock.campaignPrimary.title"
          :summary="mock.campaignPrimary.summary"
          :link="mock.campaignPrimary.link"
          :image="mock.campaignPrimary.image"
          class="rpl-site-constrain--on-all"
        />
      </template>

      <rpl-row row-gutter class="demo-main">
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-anchor-links :title="mock.anchorLinks.title" :links="mock.anchorLinks.links" />
        </rpl-col>
        <rpl-col v-if="!sidebar" cols="full" :colsBp="defaultCols">
          <rpl-card-carousel v-bind="mock.cardCarousel" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-card-navigation-featured v-bind="mock.cardNavigationFeatured" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-card-navigation v-bind="mock.cardNavigation" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-promotion v-bind="mock.cardPromotion" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-keydates v-bind="mock.cardKeydates" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-event v-bind="mock.cardEvent" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-cta v-bind="mock.cardCta" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-event v-bind="mock.cardEvent" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols">
          <rpl-card-keydates v-bind="mock.cardKeydates" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <div class="cta" :class="sidebar ? 'rpl-edge--below-l rpl-site-constrain--below-l' : 'rpl-edge--on-all rpl-site-constrain--on-all'">
            <div class="sub-content">
              edge style call to action
            </div>
          </div>
        </rpl-col>
        <rpl-col cols="full">
          <rpl-card-carousel v-bind="mock.cardCarousel" :childColsBp="sidebar ? mock.siteLayout.cardColsWithSidebar : mock.siteLayout.cardCols" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-image-gallery v-bind="mock.imageGallery" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-news-listing :title="mock.newsListing.title" :list="mock.newsListing.list" />
        </rpl-col>
        <rpl-col cols="full" :colsBp="defaultCols">
          <rpl-timeline :title="mock.timeline.title" :list="mock.timeline.list" />
        </rpl-col>
        <rpl-col cols="full">
          <rpl-document-link v-bind="mock.documentLink"></rpl-document-link>
        </rpl-col>
      </rpl-row>

      <template slot="sidebar">
        <rpl-related-links :title="mock.relatedLinks.title" :links="mock.relatedLinks.links" class="rpl-component-gutter"/>
        <rpl-whats-next :title="mock.whatsNext.title" :links="mock.whatsNext.links"  class="rpl-component-gutter" />
        <rpl-contact :title="mock.contact.title" :name="mock.contact.name" :department="mock.contact.department" :postal="mock.contact.postal" :address="mock.contact.address" :phone="mock.contact.phone" :email="mock.contact.email" :social="mock.contact.social" class="rpl-component-gutter" />
        <rpl-share-this :title="mock.shareThis.title" :url="mock.shareThis.url" class="rpl-component-gutter" />
      </template>

      <template slot="belowContent">
        <div class="rpl-site-constrain--on-all">
          <rpl-campaign-secondary :title="mock.campaignSecondaryImage.title" :summary="mock.campaignSecondaryImage.summary" :link="mock.campaignSecondaryImage.link" :image="mock.campaignSecondaryImage.image" />
        </div>
        <div class="rpl-site-constrain--on-all">
          <rpl-updated-date v-bind="mock.updatedDate"></rpl-updated-date>
        </div>
      </template>

    </rpl-page-layout>

    <template slot="footer">
      <rpl-site-footer
        :nav="mock.footer.nav"
        :links="mock.footer.links"
        :copyright="mock.footer.copyright"
        :acknowledgement="mock.footer.acknowledgement"
        />
    </template>

  </rpl-base-layout>

</template>

<script>
// This is a page for demo all components in the site layout.
// Change story knob `sidebar` can switch layout between with sidebar and without sidebar.

import { RplBaseLayout, RplPageLayout } from '@dpc-sdp/ripple-layout'
import { RplContainer, RplRow, RplCol } from '@dpc-sdp/ripple-grid'
import RplSiteFooter from '@dpc-sdp/ripple-site-footer'
import RplSiteHeader from '@dpc-sdp/ripple-site-header'

// Breadcrumb
import RplBreadcrumbs from '@dpc-sdp/ripple-breadcrumbs'

// Banner
import RplHeroBanner from '@dpc-sdp/ripple-hero-banner'

// Anchor links
import RplAnchorLinks from '@dpc-sdp/ripple-anchor-links'

// Card
import { RplCardNavigation, RplCardNavigationFeatured, RplCardPromotion, RplCardKeydates, RplCardEvent, RplCardCta, RplCardBox, RplCardEmergencyContact } from '@dpc-sdp/ripple-card'
import { RplCardCarousel } from '@dpc-sdp/ripple-card/no-ssr'

// Campaign
import RplCampaignPrimary from '@dpc-sdp/ripple-campaign-primary'
import RplCampaignSecondary from '@dpc-sdp/ripple-campaign-secondary'

// Sidebar
import RplRelatedLinks from '@dpc-sdp/ripple-related-links'
import RplWhatsNext from '@dpc-sdp/ripple-whats-next'
import RplContact from '@dpc-sdp/ripple-contact'
import RplShareThis from '@dpc-sdp/ripple-share-this'

// Alert
import { RplAlert, RplAlertBase } from '@dpc-sdp/ripple-alert'

// News Listing
import { RplNewsListing } from '@dpc-sdp/ripple-news'

// Updated Date
import RplUpdatedDate from '@dpc-sdp/ripple-updated-date'

// Miscs
import { RplImageGallery } from '@dpc-sdp/ripple-image-gallery'
import RplTimeline from '@dpc-sdp/ripple-timeline'

// Search
import { RplSearchForm } from '@dpc-sdp/ripple-search'

import RplDocumentLink from '@dpc-sdp/ripple-document-link'

export default {
  name: 'SPage',
  components: {
    // Layout
    RplBaseLayout,
    RplPageLayout,
    RplContainer,
    RplRow,
    RplCol,
    RplSiteHeader,
    RplSiteFooter,

    // Breadcrumbs
    RplBreadcrumbs,

    // Banner
    RplHeroBanner,

    // Anchor Links
    RplAnchorLinks,

    // Card
    RplCardNavigation,
    RplCardNavigationFeatured,
    RplCardPromotion,
    RplCardKeydates,
    RplCardEvent,
    RplCardCta,
    RplCardCarousel,
    RplCardEmergencyContact,
    RplCardBox,

    // Campaign
    RplCampaignPrimary,
    RplCampaignSecondary,

    // Sidebar
    RplRelatedLinks,
    RplWhatsNext,
    RplContact,
    RplShareThis,

    // Alert
    RplAlert,
    RplAlertBase,

    // News Listing
    RplNewsListing,

    // Miscs
    RplImageGallery,
    RplTimeline,

    // Updated date
    RplUpdatedDate,

    // Search
    RplSearchForm,

    // DocumentLink
    RplDocumentLink
  },
  props: {
    sidebar: Boolean,
    preview: Boolean,
    quickExit: Boolean,
    mock: Object
  },
  data () {
    return {
      defaultCols: {}
    }
  },
  created () {
    this.rplOptions.quickexit = this.quickExit
  },
  watch: {
    quickExit: function (val, oldVal) {
      this.rplOptions.quickexit = val
    }
  },
  methods: {
    // Methods for site header.
    searchFunc: function (value) {
      alert('Search for: "' + value + '"')
    }
  }
}
</script>
