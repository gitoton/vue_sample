<template>
    <div class="form-section">
        <div class="container">
            <!-- 現在のページの表示 -->
            <div class="current-num">
                <div class="num-circle" :class="chekcCurrentPage(1)">
                    {{ chekcCurrentPage(1)['passed-page'] ? "✔️" : 1 }}
                </div>
                <div class="num-circle" :class="chekcCurrentPage(1)">
                    {{ chekcCurrentPage(2)['passed-page'] ? "✔️" : 2 }}
                </div>
                <div class="num-circle" :class="chekcCurrentPage(1)">
                    {{ chekcCurrentPage(3)['passed-page'] ? "✔️" : 3 }}
                </div>
                <div class="num-circle" :class="chekcCurrentPage(1)">
                    {{ chekcCurrentPage(4)['passed-page'] ? "✔️" : 4 }}
                </div>
                <!-- １ページ目のコンテンツの表示 -->
                <div class="contact-form" v-show="currentPage === 1">
                    <div class="select">
                        <h3 class="contact-title">
                            ご相談内容をお選びください
                            <span class="optional">任意</span>
                        </h3>
                        <p class="mt20"><span class="t12"><i class="fas fa-asterisk tblue fa-fw"></i>複数選択可</span></p>
                        <div class="selects sepa2">
                            <label for="select-1" class="select-button" :class="selected(selectBox.homepage)">サイト制作</label>
                            <input type="checkbox" name="select-1" id="select-1" v-model="selectBox.homepage">
                            <label for="select-2" class="select-button" :class="selected(selectBox.system)">システム開発</label>
                            <input type="checkbox" name="select-2" id="select-2" v-model="selectBox.system">
                            <label for="select-3" class="select-button" :class="selected(selectBox.consul)">WEBコンサル</label>
                            <input type="checkbox" name="select-3" id="select-3" v-model="selectBox.consul">
                        </div>
                    </div>
                    <div class="btn_wrap">
                        <button class="b-next" @click="nextCurrentPage()">次へ</button>
                    </div>
                </div>
                <!-- ２ページ目のコンテンツの表示 -->
                <div class="content-form" v-show="currentPage === 2">
                    <div class="select">
                        <h3 class="contact-title">
                            ご相談したい内容を以下にご記入ください
                            <span class="optional">任意</span>
                        </h3>
                        <p class="t12 mt20">ご記入内容はお打ち合わせの際に参考にさせていただきます。</p>
                        <textarea class="mt20" name="contactDetail" cols="100" rows="8" maxlength="1000" v-model="contactDetail" placeholder="ホームページを新しく作成したなど。ご自由にご記入ください。"></textarea>
                    </div>
                    <div class="btn_wrap">
                        <button class="b-back" @click="prevCurrentPage()">戻る</button>
                        <button class="b-next" @click="nextCurrentPage()">次へ</button>
                    </div>
                </div>
                <!-- ３ページ目のコンテンツの表示 -->
                <div class="contact-form" v-show="currentPage === 3">
                <div class="select">
                    <h3 class="contact-title">
                        相談されたい希望日をご記入ください。
                        <span class="optional">任意</span>
                    </h3>
                    <p class="t12 mt20"><i class="fas fa-asterisk tblue fa-fw"></i>いつでも良い方は下記の「次へ」を押してください。</p>
                    <h4>曜日から選ぶ（複数回答可）</h4>
                    <div class="selects sepa3">
                        <label for="week-selecter-1" class="select-button" :class="weekSelected(selectWeek.monday)">月曜</label>
                        <input type="checkbox" id="week-select-1" name="week-select1" v-model="selectWeek.monday">
                        <label for="week-selecter-2" class="select-button" :class="weekSelected(selectWeek.tuesday)">火曜</label>
                        <input type="checkbox" id="week-select-2" name="week-select2" v-model="selectWeek.tuesday">
                        <label for="week-selecter-3" class="select-button" :class="weekSelected(selectWeek.wednesday)">水曜</label>
                        <input type="checkbox" id="week-select-3" name="week-select3" v-model="selectWeek.wednesday">
                        <label for="week-selecter-4" class="select-button" :class="weekSelected(selectWeek.thursday)">木曜</label>
                        <input type="checkbox" id="week-select-4" name="week-select4" v-model="selectWeek.thursday">
                        <label for="week-selecter-5" class="select-button" :class="weekSelected(selectWeek.friday)">金曜</label>
                        <input type="checkbox" id="week-select-5" name="week-select5" v-model="selectWeek.friday">
                    </div>

                    <div class="select-timezone">
                        <h4>時間帯から選ぶ（いずれか一つを選択）</h4>
                        <div class="select sepa3">
                            <input type="radio" id="timezone-select-1" name="timezone-select-1" v-model="timezone" value="午前">
                            <label for="timezone-select-1" class="select-button" :class="timezoneSelected('午前')">
                                午前
                            </label>
                            <input type="radio" id="timezone-select-2" name="timezone-select-2" v-model="timezone" value="午後">
                            <label for="timezone-select-2" class="select-button" :class="timezoneSelected('午後')">
                                午後
                            </label>
                            <input type="radio" id="timezone-select-3" name="timezone-select-3" v-model="timezone" value="いつでも">
                            <label for="timezone-select-3" class="select-button" :class="timezoneSelected('いつでも')">
                                いつでも
                            </label>
                        </div>
                    </div>
                    <div class="select-day mt20">
                        <h4>希望日程を選ぶ</h4>
                        <input type="date" class="mt10 pointer" name="date" v-model="date">
                    </div>
                </div>
                    <div class="btn-wrap">
                        <button class="b-back" @click="prevCurrentPage()">戻る</button>
                        <button class="b-next" @click="nextCurrentPage()">次へ</button>
                    </div>
                </div>
                <!-- ４ページ目のコンテンツの表示 -->
                <div class="contact-form" v-show="currentPage === 4">
                <div class="select">
                    <h3 classcontact-title>
                        お名前とメールアドレスを教えてください <span class="required">必須</span>
                    </h3>

                    <section class="mt20 w80">
                        <!-- 名前 -->
                        <p class=""><i class="fas fa-caret-right fa-fw"></i>名前</p>
                        <div data-field="名前" data-validate="required">
                            <input type="text" autocomplete="name" name="name" class="w100" v-model="customer.name" />
                        </div>

                        <!-- メールアドレス -->
                        <p class=""><i class="fas fa-caret-right fa-fw"></i>メールアドレス</p>
                        <div data-field="メールアドレス" 
                    </section>
                </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "AppContact"
    }
</script>

<style scoped></style>