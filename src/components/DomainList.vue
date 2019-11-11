<template>
    <div>
        <div id="main">
            <div class="container">
                <div class="row">
                    <div class="col-md">
                        <AppItemList title="Prefixos" v-bind:items="prefixes" v-on:addItem="addPrefix"
                            v-on:deleteItem="deletePrefix" />
                    </div>
                    <div class="col-md">
                        <AppItemList title="Sufixos" v-bind:items="sufixes" v-on:addItem="addSufix"
                            v-on:deleteItem="deleteSufix" />
                    </div>
                </div>
                <br>
                <h5>Domínios <span class="badge badge-info">{{ domains.length }}</span></h5>
                <div class="card">
                    <div class="card-body">
                        <ul class="list-group">
                            <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                                <div class="row">
                                    <div class="col-md">
                                        {{ domain.name }}
                                    </div>
                                    <div class="col-md text-right">
                                        <a v-bind:href="domain.checkout" target="_blank" class="btn btn-info">
                                            <span class="fa fa-shopping-cart"></span>
                                        </a>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import "bootstrap/dist/css/bootstrap.css";
    import "font-awesome/css/font-awesome.css";
    import AppItemList from './AppItemList'

    export default {
        name: 'DomainList',
        components: {
            AppItemList
        },
        data() {
            return {
                prefixes: [],
                sufixes: []
            }
        },
        methods: {
            addSufix(sufix) {
                if (sufix !== null && sufix !== undefined && sufix.length > 0 && this.sufixes.indexOf(sufix) == -1)
                    this.sufixes.push(sufix)
            },
            deleteSufix(sufix) {
                this.sufixes.splice(this.sufixes.indexOf(sufix), 1)
            },
            addPrefix(prefix) {
                if (prefix !== null && prefix !== undefined && prefix.length > 0 && this.prefixes.indexOf(prefix) == -1)
                    this.prefixes.push(prefix)
            },
            deletePrefix(prefix) {
                this.prefixes.splice(this.prefixes.indexOf(prefix), 1)
            },
        },
        computed: {
            domains() {
                const domains = []
                for (const prefix of this.prefixes) {
                    for (const sufix of this.sufixes) {
                        const name = prefix + sufix
                        const url = name.toLowerCase()
                        const checkout = `https:checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
                        domains.push({
                            name,
                            checkout
                        })
                    }
                }
                return domains
            }
        }
    }
</script>

<style lang="stylus">

</style>