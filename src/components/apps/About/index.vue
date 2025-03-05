<script setup lang="ts">
import { NDivider, NGradientText, NTag } from 'naive-ui'
import { onMounted, ref } from 'vue'
import { get } from '@/api/system/about'
import { useAppStore } from '@/store'
import srcSvglogo from '@/assets/logo.svg'
import srcGitee from '@/assets/about_image/gitee.png'
import srcGithub from '@/assets/about_image/github.png'
import srcDocker from '@/assets/about_image/docker.png'
import srcBilibili from '@/assets/about_image/bilibili.png'
import srcYoutube from '@/assets/about_image/youtube.png'
import srcQQGroupQR from '@/assets/about_image/qq_group_qr2.png'
import { RoundCardModal } from '@/components/common'

interface Version {
  versionName: string
  versionCode: number
}

const appStore = useAppStore()
const versionName = ref('')
const qqGroupQRShow = ref(false)
const frontVersion = import.meta.env.VITE_APP_VERSION || 'unknown'

onMounted(() => {
  get<Version>().then((res) => {
    if (res.code === 0)
      versionName.value = res.data.versionName
  })
})
</script>

<template>
  <div class="pt-5">
    <div class="flex flex-col items-center justify-center">
      <img :src="srcSvglogo" width="100" height="100" alt="">
      <div class="text-3xl font-semibold">
        {{ $t('common.appName') }}
      </div>
      <div class="text-xl">
        <NGradientText type="info">
          <a class="font-semibold" :title="$t('apps.about.viewUpdateLog')" >v{{ versionName }}</a>
        </NGradientText>
      </div>
      <div class="mt-2">
        <a>{{ $t('apps.about.checkUpdate') }}</a>
      </div>
    </div>
  </div>
</template>

<style>
.link{
    color:rgb(0, 89, 255)
}
</style>
