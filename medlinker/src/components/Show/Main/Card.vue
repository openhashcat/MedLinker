<template>
    <b-card no-body class="mb-1">
        <b-card-header header-tag="header" class="p-1" role="tab">
            <h5 class="mb-0">
                <b-button block href="#" v-b-toggle="id">{{ name }}</b-button>
            </h5>
        </b-card-header>
        <b-collapse v-bind:id="id" v-bind:visible="visible" accordion="my-accordion" role="tabpanel">
            <b-card-body>
                <b-card-text>
                    <b-alert show variant="success">
                        <p>
                        文章哈希：{{ id }}
                        </p>
                        <hr />
                        <p class="mb-0">
                        文章记录区块高度：<a :href="`https://rinkeby.etherscan.io/block/${block_number}`">{{ block_number }}</a>
                        </p>
                    </b-alert>
                    <p>
                    作者： {{ author }}
                    </p>
                    <p>
                    可用链接：
                    </p>
                    <b-list-group >
                        <b-list-group-item v-for="link in urls" :key="link">
                            <a :href="link">{{ display(link) }} ：《{{ name }}》</a>
                        </b-list-group-item>
                    </b-list-group>
                </b-card-text>
            </b-card-body>
        </b-collapse>
    </b-card>
</template>

<script>
import Url from 'url-parse';

const map = {
    'github.com': 'Github',
    'www.jianshu.com': '简书',
    'mp.weixin.qq.com': '微信公众号',
    'tiannian.me': '博客-念者'
}

export default {
    props: ['id' ,'name', 'author', 'visible', 'block_number', 'urls'],
    methods:{
        display(url) {
            let u = new Url(url);
            return map[u.host];
        }
    }
}
</script>
