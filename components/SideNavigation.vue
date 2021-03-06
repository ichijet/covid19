<template>
  <div class="SideNavigation">
    <div class="SideNavigation-HeadingContainer sp-flex">
      <v-icon
        class="SideNavigation-HeadingIcon sp-inline-block"
        :aria-label="$t('Navi Open')"
        @click="openNavi"
      >
        mdi-menu
      </v-icon>
      <nuxt-link to="/" class="SideNavigation-HeadingLink">
        <div class="SideNavigation-Logo">
          <img src="/logo.svg" :alt="$t('Kanagawa')" />
        </div>
        <h1 class="SideNavigation-Heading">
          {{ $t('COVID-19') }}<br />{{ $t('Measures site') }}
        </h1>
      </nuxt-link>
    </div>
    <v-divider class="SideNavigation-HeadingDivider" />
    <div class="sp-none" :class="{ open: isNaviOpen }">
      <v-icon
        class="SideNavigation-ListContainerIcon sp-inline-block"
        :aria-label="$t('Navi Close')"
        @click="closeNavi"
      >
        mdi-close
      </v-icon>
      <v-list :flat="true">
        <v-container
          v-for="(item, i) in items"
          :key="i"
          class="SideNavigation-ListItemContainer"
          @click="closeNavi"
        >
          <ListItem :link="item.link" :icon="item.icon" :title="item.title" />
          <v-divider v-show="item.divider" class="SideNavigation-Divider" />
        </v-container>
      </v-list>
      <div class="SideNavigation-Footer">
        <div class="SideNavigation-SocialLinkContainer">
          <a
            href="https://www.openkawasaki.org/"
            target="_blank"
            rel="noopener"
          >
            <img src="/icon.png" alt="Twitter" />
          </a>
          <a
            href="https://www.facebook.com/openkawasaki/"
            target="_blank"
            rel="noopener"
          >
            <img src="/facebook.png" alt="Facebook" />
          </a>
        </div>
        <small class="SideNavigation-Copyright" lang="en">
          Powered by Open Kawasaki / Code for Kawasaki
        </small>
      </div>
    </div>
  </div>
</template>

<i18n>
{
  "ja": {
    "Navi Open": "サイドメニュー項目を開く",
    "Navi Close": "サイドメニュー項目を閉じる",
    "Kanagawa": "神奈川県",
    "COVID-19": "新型コロナウイルス感染症",
    "Measures site": "神奈川県 対策サイト",
    "Kanagawa Government": "神奈川県",
    "The latest updates": "神奈川県内の最新感染動向",
    "If you have any symptoms": "新型コロナウイルス感染症が心配なときに",
    "for Families with children": "お子様をお持ちの皆様へ",
    "for Citizens": "県民の皆様へ",
    "about COVID-19": "新型コロナウイルス感染症について",
    "for Enterprises and Employees": "企業の皆様・はたらく皆様へ",
    "Official statements from Task Force": "神奈川県新型コロナウイルス感染症対策本部報",
    "Cancelled public events": "神奈川県主催等 中止又は延期するイベント等",
    "Government official website": "神奈川県公式ホームページ",
    "Government official line": "神奈川県公式LINEアカウント",
    "Government official twitter": "神奈川県公式Twitterアカウント",
    "Message from Governor Kuroiwa": "知事からのメッセージ",
    "About us": "当サイトについて"
  }
}
</i18n>

<script>
import ListItem from '@/components/ListItem'

export default {
  components: {
    ListItem
  },
  props: {
    isNaviOpen: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    items() {
      return [
        {
          icon: 'mdi-chart-timeline-variant',
          title: this.$t('The latest updates'),
          link: '/'
        },
        {
          icon: 'covid',
          title: this.$t('about COVID-19'),
          link:
            'https://www.pref.kanagawa.jp/docs/ga4/bukanshi/bukan_200114.html',
          divider: true
        },
        {
          icon: 'parent',
          title: this.$t('for Families with children'),
          link: '/parent'
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('for Citizens'),
          link:
            'https://www.pref.kanagawa.jp/docs/ga4/bukanshi/bukan_200114.html'
        },
        {
          icon: 'mdi-domain',
          title: this.$t('for Enterprises and Employees'),
          link: '/worker',
          divider: true
        },
        {
          title: this.$t('Cancelled public events'),
          link: 'https://www.pref.kanagawa.jp/docs/ie2/event/2020spring.html'
        },
        {
          title: this.$t('Message from Governor Kuroiwa'),
          link:
            'https://www.pref.kanagawa.jp/docs/ga4/bukanshi/bukan_200114.html#chiji'
        },
        {
          title: this.$t('Government official website'),
          link: 'https://www.pref.kanagawa.jp/'
        },
        {
          title: this.$t('Government official line'),
          link: 'https://lin.ee/BMlBaDg'
        },
        {
          title: this.$t('Government official twitter'),
          link: 'https://twitter.com/KanagawaPref_PR',
          divider: true
        },
        {
          title: this.$t('About us'),
          link: '/about'
        }
      ]
    }
  },
  methods: {
    openNavi() {
      this.$emit('openNavi')
    },
    closeNavi() {
      this.$emit('closeNavi')
    }
  }
}
</script>

<style lang="scss" scoped>
.SideNavigation {
  position: relative;
  height: 100%;
  background: $white;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.15);
  &-HeadingContainer {
    padding: 1.25em 0 1.25em 1.25em;
    align-items: center;
    @include lessThan($small) {
      padding: 7px 0 7px 20px;
    }
  }
  &-HeadingIcon {
    display: none;
    margin-right: 16px;
  }
  &-HeadingLink {
    @include lessThan($small) {
      display: flex;
      align-items: center;
    }
    text-decoration: none;
  }
  &-ListContainerIcon {
    display: none;
    margin: 24px 16px 0;
  }
  &-ListItemContainer {
    padding: 2px 20px;
  }
  &-Logo {
    margin: 20px 16px 0 0;
    width: 110px;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-Heading {
    margin-top: 8px;
    font-size: 13px;
    color: #898989;
    padding: 0.5em 0;
    text-decoration: none;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-HeadingDivider {
    margin: 0px 20px 4px;
    @include lessThan($small) {
      display: none;
    }
  }
  &-Divider {
    margin: 12px 0;
  }
  &-Footer {
    padding: 20px;
    background-color: $white;
  }
  &-SocialLinkContainer {
    display: flex;
    & img {
      width: 30px;
      &:first-of-type {
        margin-right: 10px;
      }
    }
  }
  &-Copyright {
    display: block;
    margin-top: 10px;
    font-size: 8px;
    line-height: 1.2;
    color: $gray-1;
    font-weight: bold;
  }
}
.open {
  @include lessThan($small) {
    position: absolute;
    top: 0;
    left: 0;
    display: block !important;
    width: 100%;
    z-index: 100;
    background-color: $white;
  }
}
@include lessThan($small) {
  .sp-flex {
    display: flex;
  }
  .sp-inline-block {
    display: inline-block;
  }
  .sp-none {
    display: none;
  }
}
</style>
