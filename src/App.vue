<template>
  <div class="app-container">
    <div class="table-container">
      <Table
        :data="list"
        :columns="columns"
        :key-field="'id'"
        :height="32"
        :scroll="scroll"
      />
    </div>
    <div class="options-container">
      <button @click="scrollTable">Horizontal scroll {{ scrollList[index + 1] }}</button>
      <p>
        scroll horizontally (drag or button)
        <br>
        and then scroll vertically
      </p>
    </div>
  </div>
</template>

<script>
// import RecycleScroller from ''
// import TheWelcome from './components/TheWelcome.vue'

import Table from "@/components/Table.vue";

export default {
  name: 'App',
  components: {Table},
  data () {
    return {
      list: [
        {"id":1,"name":"Anderson","doubleName":"Anderson-Anderson","elseName":"AndersonAndersonAnderson"},
        {"id":2,"name":"Ashwoon","doubleName":"Ashwoon-Ashwoon","elseName":"AshwoonAshwoonAshwoon"},
        {"id":3,"name":"Aikin","doubleName":"Aikin-Aikin","elseName":"AikinAikinAikin"},
        {"id":4,"name":"Bateman","doubleName":"Bateman-Bateman","elseName":"BatemanBatemanBateman"},
        {"id":5,"name":"Bongard","doubleName":"Bongard-Bongard","elseName":"BongardBongardBongard"},{"id":6,"name":"Bowers","doubleName":"Bowers-Bowers","elseName":"BowersBowersBowers"},{"id":7,"name":"Boyd","doubleName":"Boyd-Boyd","elseName":"BoydBoydBoyd"},{"id":8,"name":"Cannon","doubleName":"Cannon-Cannon","elseName":"CannonCannonCannon"},{"id":9,"name":"Cast","doubleName":"Cast-Cast","elseName":"CastCastCast"},{"id":10,"name":"Deitz","doubleName":"Deitz-Deitz","elseName":"DeitzDeitzDeitz"},{"id":11,"name":"Dewalt","doubleName":"Dewalt-Dewalt","elseName":"DewaltDewaltDewalt"},{"id":12,"name":"Ebner","doubleName":"Ebner-Ebner","elseName":"EbnerEbnerEbner"},{"id":13,"name":"Frick","doubleName":"Frick-Frick","elseName":"FrickFrickFrick"},{"id":14,"name":"Hancock","doubleName":"Hancock-Hancock","elseName":"HancockHancockHancock"},{"id":15,"name":"Haworth","doubleName":"Haworth-Haworth","elseName":"HaworthHaworthHaworth"},{"id":16,"name":"Hesch","doubleName":"Hesch-Hesch","elseName":"HeschHeschHesch"},{"id":17,"name":"Hoffman","doubleName":"Hoffman-Hoffman","elseName":"HoffmanHoffmanHoffman"},{"id":18,"name":"Kassing","doubleName":"Kassing-Kassing","elseName":"KassingKassingKassing"},{"id":19,"name":"Knutson","doubleName":"Knutson-Knutson","elseName":"KnutsonKnutsonKnutson"},{"id":20,"name":"Lawless","doubleName":"Lawless-Lawless","elseName":"LawlessLawlessLawless"},{"id":21,"name":"Lawicki","doubleName":"Lawicki-Lawicki","elseName":"LawickiLawickiLawicki"},{"id":22,"name":"Mccord","doubleName":"Mccord-Mccord","elseName":"MccordMccordMccord"},{"id":23,"name":"McCormack","doubleName":"McCormack-McCormack","elseName":"McCormackMcCormackMcCormack"},{"id":24,"name":"Miller","doubleName":"Miller-Miller","elseName":"MillerMillerMiller"},{"id":25,"name":"Myers","doubleName":"Myers-Myers","elseName":"MyersMyersMyers"},{"id":26,"name":"Nugent","doubleName":"Nugent-Nugent","elseName":"NugentNugentNugent"},{"id":27,"name":"Ortiz","doubleName":"Ortiz-Ortiz","elseName":"OrtizOrtizOrtiz"},{"id":28,"name":"Orwig","doubleName":"Orwig-Orwig","elseName":"OrwigOrwigOrwig"},{"id":29,"name":"Ory","doubleName":"Ory-Ory","elseName":"OryOryOry"},{"id":30,"name":"Paiser","doubleName":"Paiser-Paiser","elseName":"PaiserPaiserPaiser"},{"id":31,"name":"Pak","doubleName":"Pak-Pak","elseName":"PakPakPak"},{"id":32,"name":"Pettigrew","doubleName":"Pettigrew-Pettigrew","elseName":"PettigrewPettigrewPettigrew"},{"id":33,"name":"Quinn","doubleName":"Quinn-Quinn","elseName":"QuinnQuinnQuinn"},{"id":34,"name":"Quizoz","doubleName":"Quizoz-Quizoz","elseName":"QuizozQuizozQuizoz"},{"id":35,"name":"Ramachandran","doubleName":"Ramachandran-Ramachandran","elseName":"RamachandranRamachandranRamachandran"},{"id":36,"name":"Resnick","doubleName":"Resnick-Resnick","elseName":"ResnickResnickResnick"},{"id":37,"name":"Sagar","doubleName":"Sagar-Sagar","elseName":"SagarSagarSagar"},{"id":38,"name":"Schickowski","doubleName":"Schickowski-Schickowski","elseName":"SchickowskiSchickowskiSchickowski"},{"id":39,"name":"Schiebel","doubleName":"Schiebel-Schiebel","elseName":"SchiebelSchiebelSchiebel"},{"id":40,"name":"Sellon","doubleName":"Sellon-Sellon","elseName":"SellonSellonSellon"},{"id":41,"name":"Severson","doubleName":"Severson-Severson","elseName":"SeversonSeversonSeverson"},{"id":42,"name":"Shaffer","doubleName":"Shaffer-Shaffer","elseName":"ShafferShafferShaffer"},{"id":43,"name":"Solberg","doubleName":"Solberg-Solberg","elseName":"SolbergSolbergSolberg"},{"id":44,"name":"Soloman","doubleName":"Soloman-Soloman","elseName":"SolomanSolomanSoloman"},{"id":45,"name":"Sonderling","doubleName":"Sonderling-Sonderling","elseName":"SonderlingSonderlingSonderling"},{"id":46,"name":"Soukup","doubleName":"Soukup-Soukup","elseName":"SoukupSoukupSoukup"},{"id":47,"name":"Soulis","doubleName":"Soulis-Soulis","elseName":"SoulisSoulisSoulis"},{"id":48,"name":"Stahl","doubleName":"Stahl-Stahl","elseName":"StahlStahlStahl"},{"id":49,"name":"Sweeney","doubleName":"Sweeney-Sweeney","elseName":"SweeneySweeneySweeney"},{"id":50,"name":"Tandy","doubleName":"Tandy-Tandy","elseName":"TandyTandyTandy"},{"id":51,"name":"Trebil","doubleName":"Trebil-Trebil","elseName":"TrebilTrebilTrebil"},{"id":52,"name":"Trusela","doubleName":"Trusela-Trusela","elseName":"TruselaTruselaTrusela"},{"id":53,"name":"Trussel","doubleName":"Trussel-Trussel","elseName":"TrusselTrusselTrussel"},{"id":54,"name":"Turco","doubleName":"Turco-Turco","elseName":"TurcoTurcoTurco"},{"id":55,"name":"Uddin","doubleName":"Uddin-Uddin","elseName":"UddinUddinUddin"},{"id":56,"name":"Uflan","doubleName":"Uflan-Uflan","elseName":"UflanUflanUflan"},{"id":57,"name":"Ulrich","doubleName":"Ulrich-Ulrich","elseName":"UlrichUlrichUlrich"},{"id":58,"name":"Upson","doubleName":"Upson-Upson","elseName":"UpsonUpsonUpson"},{"id":59,"name":"Vader","doubleName":"Vader-Vader","elseName":"VaderVaderVader"},{"id":60,"name":"Vail","doubleName":"Vail-Vail","elseName":"VailVailVail"},{"id":61,"name":"Valente","doubleName":"Valente-Valente","elseName":"ValenteValenteValente"},{"id":62,"name":"Van Zandt","doubleName":"Van Zandt-Van Zandt","elseName":"Van ZandtVan ZandtVan Zandt"},{"id":63,"name":"Vanderpoel","doubleName":"Vanderpoel-Vanderpoel","elseName":"VanderpoelVanderpoelVanderpoel"},{"id":64,"name":"Ventotla","doubleName":"Ventotla-Ventotla","elseName":"VentotlaVentotlaVentotla"},{"id":65,"name":"Vogal","doubleName":"Vogal-Vogal","elseName":"VogalVogalVogal"},{"id":66,"name":"Wagle","doubleName":"Wagle-Wagle","elseName":"WagleWagleWagle"},{"id":67,"name":"Wagner","doubleName":"Wagner-Wagner","elseName":"WagnerWagnerWagner"},{"id":68,"name":"Wakefield","doubleName":"Wakefield-Wakefield","elseName":"WakefieldWakefieldWakefield"},{"id":69,"name":"Weinstein","doubleName":"Weinstein-Weinstein","elseName":"WeinsteinWeinsteinWeinstein"},{"id":70,"name":"Weiss","doubleName":"Weiss-Weiss","elseName":"WeissWeissWeiss"},{"id":71,"name":"Woo","doubleName":"Woo-Woo","elseName":"WooWooWoo"},{"id":72,"name":"Yang","doubleName":"Yang-Yang","elseName":"YangYangYang"},{"id":73,"name":"Yates","doubleName":"Yates-Yates","elseName":"YatesYatesYates"},{"id":74,"name":"Yocum","doubleName":"Yocum-Yocum","elseName":"YocumYocumYocum"},{"id":75,"name":"Zeaser","doubleName":"Zeaser-Zeaser","elseName":"ZeaserZeaserZeaser"},{"id":76,"name":"Zeller","doubleName":"Zeller-Zeller","elseName":"ZellerZellerZeller"},{"id":77,"name":"Ziegler","doubleName":"Ziegler-Ziegler","elseName":"ZieglerZieglerZiegler"},{"id":78,"name":"Bauer","doubleName":"Bauer-Bauer","elseName":"BauerBauerBauer"},{"id":79,"name":"Baxster","doubleName":"Baxster-Baxster","elseName":"BaxsterBaxsterBaxster"},{"id":80,"name":"Casal","doubleName":"Casal-Casal","elseName":"CasalCasalCasal"},{"id":81,"name":"Cataldi","doubleName":"Cataldi-Cataldi","elseName":"CataldiCataldiCataldi"},{"id":82,"name":"Caswell","doubleName":"Caswell-Caswell","elseName":"CaswellCaswellCaswell"},{"id":83,"name":"Celedon","doubleName":"Celedon-Celedon","elseName":"CeledonCeledonCeledon"},{"id":84,"name":"Chambers","doubleName":"Chambers-Chambers","elseName":"ChambersChambersChambers"},{"id":85,"name":"Chapman","doubleName":"Chapman-Chapman","elseName":"ChapmanChapmanChapman"},{"id":86,"name":"Christensen","doubleName":"Christensen-Christensen","elseName":"ChristensenChristensenChristensen"},{"id":87,"name":"Darnell","doubleName":"Darnell-Darnell","elseName":"DarnellDarnellDarnell"},{"id":88,"name":"Davidson","doubleName":"Davidson-Davidson","elseName":"DavidsonDavidsonDavidson"},{"id":89,"name":"Davis","doubleName":"Davis-Davis","elseName":"DavisDavisDavis"},{"id":90,"name":"DeLorenzo","doubleName":"DeLorenzo-DeLorenzo","elseName":"DeLorenzoDeLorenzoDeLorenzo"},{"id":91,"name":"Dinkins","doubleName":"Dinkins-Dinkins","elseName":"DinkinsDinkinsDinkins"},{"id":92,"name":"Doran","doubleName":"Doran-Doran","elseName":"DoranDoranDoran"},{"id":93,"name":"Dugelman","doubleName":"Dugelman-Dugelman","elseName":"DugelmanDugelmanDugelman"},{"id":94,"name":"Dugan","doubleName":"Dugan-Dugan","elseName":"DuganDuganDugan"},{"id":95,"name":"Duffman","doubleName":"Duffman-Duffman","elseName":"DuffmanDuffmanDuffman"},{"id":96,"name":"Eastman","doubleName":"Eastman-Eastman","elseName":"EastmanEastmanEastman"},{"id":97,"name":"Ferro","doubleName":"Ferro-Ferro","elseName":"FerroFerroFerro"},{"id":98,"name":"Ferry","doubleName":"Ferry-Ferry","elseName":"FerryFerryFerry"},{"id":99,"name":"Fletcher","doubleName":"Fletcher-Fletcher","elseName":"FletcherFletcherFletcher"},{"id":100,"name":"Fietzer","doubleName":"Fietzer-Fietzer","elseName":"FietzerFietzerFietzer"},{"id":101,"name":"Hylan","doubleName":"Hylan-Hylan","elseName":"HylanHylanHylan"},{"id":102,"name":"Hydinger","doubleName":"Hydinger-Hydinger","elseName":"HydingerHydingerHydinger"},{"id":103,"name":"Illingsworth","doubleName":"Illingsworth-Illingsworth","elseName":"IllingsworthIllingsworthIllingsworth"},{"id":104,"name":"Ingram","doubleName":"Ingram-Ingram","elseName":"IngramIngramIngram"},{"id":105,"name":"Irwin","doubleName":"Irwin-Irwin","elseName":"IrwinIrwinIrwin"},{"id":106,"name":"Jagtap","doubleName":"Jagtap-Jagtap","elseName":"JagtapJagtapJagtap"},{"id":107,"name":"Jenson","doubleName":"Jenson-Jenson","elseName":"JensonJensonJenson"},{"id":108,"name":"Johnson","doubleName":"Johnson-Johnson","elseName":"JohnsonJohnsonJohnson"},{"id":109,"name":"Johnsen","doubleName":"Johnsen-Johnsen","elseName":"JohnsenJohnsenJohnsen"},{"id":110,"name":"Jones","doubleName":"Jones-Jones","elseName":"JonesJonesJones"},{"id":111,"name":"Jurgenson","doubleName":"Jurgenson-Jurgenson","elseName":"JurgensonJurgensonJurgenson"},{"id":112,"name":"Kalleg","doubleName":"Kalleg-Kalleg","elseName":"KallegKallegKalleg"},{"id":113,"name":"Kaskel","doubleName":"Kaskel-Kaskel","elseName":"KaskelKaskelKaskel"},{"id":114,"name":"Keller","doubleName":"Keller-Keller","elseName":"KellerKellerKeller"},{"id":115,"name":"Leisinger","doubleName":"Leisinger-Leisinger","elseName":"LeisingerLeisingerLeisinger"},{"id":116,"name":"LePage","doubleName":"LePage-LePage","elseName":"LePageLePageLePage"},{"id":117,"name":"Lewis","doubleName":"Lewis-Lewis","elseName":"LewisLewisLewis"},{"id":118,"name":"Linde","doubleName":"Linde-Linde","elseName":"LindeLindeLinde"},{"id":119,"name":"Lulloff","doubleName":"Lulloff-Lulloff","elseName":"LulloffLulloffLulloff"},{"id":120,"name":"Maki","doubleName":"Maki-Maki","elseName":"MakiMakiMaki"},{"id":121,"name":"Martin","doubleName":"Martin-Martin","elseName":"MartinMartinMartin"},{"id":122,"name":"McGinnis","doubleName":"McGinnis-McGinnis","elseName":"McGinnisMcGinnisMcGinnis"},{"id":123,"name":"Mills","doubleName":"Mills-Mills","elseName":"MillsMillsMills"},{"id":124,"name":"Moody","doubleName":"Moody-Moody","elseName":"MoodyMoodyMoody"},{"id":125,"name":"Moore","doubleName":"Moore-Moore","elseName":"MooreMooreMoore"},{"id":126,"name":"Napier","doubleName":"Napier-Napier","elseName":"NapierNapierNapier"},{"id":127,"name":"Nelson","doubleName":"Nelson-Nelson","elseName":"NelsonNelsonNelson"},{"id":128,"name":"Norquist","doubleName":"Norquist-Norquist","elseName":"NorquistNorquistNorquist"},{"id":129,"name":"Nuttle","doubleName":"Nuttle-Nuttle","elseName":"NuttleNuttleNuttle"},{"id":130,"name":"Olson","doubleName":"Olson-Olson","elseName":"OlsonOlsonOlson"},{"id":131,"name":"Ostrander","doubleName":"Ostrander-Ostrander","elseName":"OstranderOstranderOstrander"},{"id":132,"name":"Reamer","doubleName":"Reamer-Reamer","elseName":"ReamerReamerReamer"},{"id":133,"name":"Reardon","doubleName":"Reardon-Reardon","elseName":"ReardonReardonReardon"},{"id":134,"name":"Reyes","doubleName":"Reyes-Reyes","elseName":"ReyesReyesReyes"},{"id":135,"name":"Rice","doubleName":"Rice-Rice","elseName":"RiceRiceRice"},{"id":136,"name":"Ripka","doubleName":"Ripka-Ripka","elseName":"RipkaRipkaRipka"},{"id":137,"name":"Roberts","doubleName":"Roberts-Roberts","elseName":"RobertsRobertsRoberts"},{"id":138,"name":"Rogers","doubleName":"Rogers-Rogers","elseName":"RogersRogersRogers"},{"id":139,"name":"Root","doubleName":"Root-Root","elseName":"RootRootRoot"},{"id":140,"name":"Sandstrom","doubleName":"Sandstrom-Sandstrom","elseName":"SandstromSandstromSandstrom"},{"id":141,"name":"Sawyer","doubleName":"Sawyer-Sawyer","elseName":"SawyerSawyerSawyer"},{"id":142,"name":"Schlicht","doubleName":"Schlicht-Schlicht","elseName":"SchlichtSchlichtSchlicht"},{"id":143,"name":"Schmitt","doubleName":"Schmitt-Schmitt","elseName":"SchmittSchmittSchmitt"},{"id":144,"name":"Schwager","doubleName":"Schwager-Schwager","elseName":"SchwagerSchwagerSchwager"},{"id":145,"name":"Schutz","doubleName":"Schutz-Schutz","elseName":"SchutzSchutzSchutz"},{"id":146,"name":"Schuster","doubleName":"Schuster-Schuster","elseName":"SchusterSchusterSchuster"},{"id":147,"name":"Tapia","doubleName":"Tapia-Tapia","elseName":"TapiaTapiaTapia"},{"id":148,"name":"Thompson","doubleName":"Thompson-Thompson","elseName":"ThompsonThompsonThompson"},{"id":149,"name":"Tiernan","doubleName":"Tiernan-Tiernan","elseName":"TiernanTiernanTiernan"},
        {"id":150,"name":"Tisler","doubleName":"Tisler-Tisler","elseName":"TislerTislerTisler"}
      ],
      columns: [
        { key: 'id', title: 'ID' },
        { key: 'name', title: 'Name'},
        { key: 'doubleName', title: 'Double Name'},
        { key: 'elseName', title: 'Else Name' }
      ],
      scroll: 0,
      scrollList: [200, 350, 20],
      index: 0
    }
  },
  methods: {
    scrollTable () {
      this.index === 2 ? this.index = 0 : this.index++
      this.scroll = this.scrollList[this.index]
    }
  }
}
</script>

<style scoped>
.app-container {
  display: flex;
  align-items: baseline;
}
.table-container {
  display: flex;
  overflow: hidden;
  height: calc(100vh - 100px);
  width: 600px;
  border: 4px solid darkgrey;
}
.options-container {
  margin-left: 50px;
}
</style>
