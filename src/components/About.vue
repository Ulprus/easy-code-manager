<template>
    <div class="fss_support">
        <el-row :gutter="20">
            <el-col :sm="24" :md="12">
                <div class="fss_about">
                    <div class="fss_header">About</div>
                    <div class="fss_content">
                        <p>
                            <a href="https://fluentsnippets.com" target="_blank" rel="noopener">FluentSnippets</a> is The High-Performance Code Snippets Plugin for WordPress.
                            It is built for speed and security. All code snippets are stored in the file system and load just like a regular feature plugin. No database query, it’s secure and native.
                        </p>
                        <div>
                            <p>FluentSMTP is built using the following open-sorce libraries and software</p>
                            <ul style="list-style: disc;margin-left: 30px;">
                                <li>VueJS</li>
                                <li>Vue Router</li>
                                <li>codemirror</li>
                                <li>dayjs</li>
                                <li>fuse.js</li>
                                <li>lodash</li>
                                <li>element-plus</li>
                            </ul>
                            <p>
                                If you find an issue or have a suggestion please <a target="_blank" rel="nofollow"
                                                                                    href="https://github.com/WPManageNinja/easy-code-manager/issues">open
                                an issue on GitHub</a>.
                                <br/>If you are a developer and would like to contribute to the project, Please <a
                                target="_blank" rel="nofollow" href="https://github.com/WPManageNinja/easy-code-manager/">contribute
                                on GitHub</a>.
                            </p>
                            <p>Please <a target="_blank" rel="noopener" href="http://fluentsnippets.com/docs">read the
                                documentation here</a></p>
                        </div>
                    </div>
                </div>
            </el-col>
            <el-col :sm="24" :md="12">
                <div v-if="plugin || installed_info">
                    <div v-loading="installing" element-loading-text="Installing... Please wait" class="fss_about">
                        <div class="fss_header">Recommended Plugin</div>
                        <div class="fss_content">
                            <div v-if="installed_info" class="install_success">
                                <h3>{{ installed_message }}</h3>
                                <a class="el-button el-button--success installed_dashboard_url"
                                   :href="installed_info.admin_url">{{ installed_info.title }}</a>
                            </div>
                            <div v-else class="fss_plugin_block">
                                <div class="fss_plugin_title">
                                    <h3>{{ plugin.title }}</h3>
                                    <p>{{ plugin.subtitle }}</p>
                                </div>
                                <div class="fss_plugin_body">
                                    <div v-html="plugin.description"></div>
                                    <div class="fss_install_btn">
                                        <el-button v-if="!appVars.disable_installation"
                                                   @click="installPlugin(plugin.slug)"
                                                   :class="plugin.btn_class" type="success">{{ plugin.btn_text }}
                                        </el-button>
                                        <a v-else :href="plugin.plugin_url" target="_blank" rel="noopener"
                                           class="el-button el-button--success fss_ninjatables_btn">
                                            <span>View {{ plugin.title }}</span>
                                        </a>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="fss_about">
                    <div class="fss_header">Community</div>
                    <div class="fss_content">
                        <p>FluentSnippets is powered by community. We listen to our community users and build products that
                            add values to businesses and save time.</p>
                        <p>Join our communities and participate in great conversations.</p>
                        <ul style="list-style: disc;margin-left: 30px;">
                            <li>
                                <a target="_blank" rel="nofollow" href="https://www.facebook.com/groups/fluentforms">Join
                                    FluentForms Facebook Community</a>
                            </li>
                            <li>
                                <a target="_blank" rel="nofollow" href="https://www.facebook.com/groups/fluentcrm">Join
                                    FluentCRM Facebook Community</a>
                            </li>
                            <li>
                                <a target="_blank" rel="nofollow"
                                   href="https://wordpress.org/support/plugin/easy-code-manager/reviews/?filter=5">Write a
                                    review (really appreciate 😊)</a>
                            </li>
                            <li>
                                <a target="_blank" rel="noopener" href="http://fluentsnippets.com/docs">Read the
                                    documentation</a>
                            </li>
                        </ul>
                    </div>
                </div>
            </el-col>
        </el-row>
    </div>
</template>

<script type="text/babel">
import sample from 'lodash/sample';

export default {
    name: 'FluentMailSupport',
    data() {
        return {
            plugins: {
                fluentsmtp: {
                    slug: 'fluent-smtp',
                    title: 'Fluent SMTP',
                    subtitle: 'WP Mail SMTP, Amazon SES, SendGrid, MailGun and Any SMTP Connector Plugin',
                    description: '<p><a href="https://wordpress.org/plugins/fluent-smtp" target="_blank" rel="nofollow">FluentSMTP</a> plugin fixes your email delivery issue by connecting WordPress Mail with your email service providers. These integrations are native, so it will send the emails super-fast. It\'s free and will be always free.</p>',
                    btn_text: 'Install Fluent SMTP (Free)',
                    btn_class: '',
                    plugin_url: 'https://wordpress.org/plugins/fluent-smtp'
                },
                fluentform: {
                    slug: 'fluentform',
                    title: 'Fluent Forms',
                    subtitle: 'Fastest Contact Form Builder Plugin for WordPress',
                    description: '<p><a href="https://wordpress.org/plugins/fluentform" target="_blank" rel="nofollow">Fluent Forms</a> is the ultimate user-friendly, fast, customizable drag-and-drop WordPress Contact Form Plugin that offers you all the premium features, plus many more completely unique additional features.</p>',
                    btn_text: 'Install Fluent Forms (Free)',
                    btn_class: '',
                    plugin_url: 'https://wordpress.org/plugins/fluentform'
                },
                fluent_crm: {
                    slug: 'fluent-crm',
                    title: 'FluentCRM',
                    subtitle: 'Email Marketing Automation and CRM Plugin for WordPress',
                    description: '<p><a href="https://wordpress.org/plugins/fluent-crm/" target="_blank" rel="nofollow">FluentCRM</a> is the best and complete feature-rich Email Marketing & CRM solution. It is also the simplest and fastest CRM and Marketing Plugin on WordPress. Manage your customer relationships, build your email lists, send email campaigns, build funnels, and make more profit and increase your conversion rates. (Yes, It’s Free!)</p>',
                    btn_text: 'Install FluentCRM (Free)',
                    btn_class: 'fss_fluentcrm_btn',
                    plugin_url: 'https://wordpress.org/plugins/fluent-crm/'
                },
                ninja_tables: {
                    slug: 'ninja-tables',
                    title: 'Ninja Tables',
                    subtitle: 'Best WP DataTables Plugin for WordPress',
                    description: '<p>Looking for a WordPress table plugin for your website? Then you’re in the right place.</p>' +
                        '<p>Meet <a href="https://wordpress.org/plugins/ninja-tables/" target="_blank" rel="nofollow">Ninja Tables</a>, the best WP table plugin that comes with all the solutions to the problems you face while creating tables on your posts/pages.</p>',
                    btn_text: 'Install Ninja Tables (Free)',
                    btn_class: 'fss_ninjatables_btn',
                    plugin_url: 'https://wordpress.org/plugins/ninja-tables/'
                }
            },
            installing: false,
            installed_info: false,
            installed_message: '',
            contributors: [],
            contributorsLoading: false
        }
    },
    computed: {
        plugin() {
            if (this.appVars.disable_recommendation) {
                return false;
            }
            const recommended = [];

            if (!this.appVars.has_fluentsmtp) {
                recommended.push(this.plugins.has_fluentsmtp)
            }

            if (!this.appVars.has_fluentform) {
                recommended.push(this.plugins.fluentform)
            }
            if (!this.appVars.has_ninja_tables) {
                recommended.push(this.plugins.ninja_tables)
            }
            if (!this.appVars.has_fluentcrm) {
                recommended.push(this.plugins.fluent_crm)
            }
            if (!recommended.length) {
                return false;
            }
            return sample(recommended);
        }
    },
    methods: {
        installPlugin(slug) {
            this.installing = true;
            this.$post('install_plugin', {
                plugin_slug: slug
            })
                .then(response => {
                    this.installed_info = response.info;
                    this.installed_message = response.message;
                })
                .catch((error) => {
                    this.$handleError(error);
                })
                .finally(() => {
                    this.installing = false;
                });
        }
    }
}
</script>
