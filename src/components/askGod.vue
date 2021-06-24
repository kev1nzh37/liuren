<template>
	<div class="box">
		<div class="title">小六壬·活数起课法</div>
		<div class="input-wrapper">
			<span>取数：</span>

			<el-popover
				placement="top-start"
				title="活数起课法"
				:width="400"
				trigger="hover"
				content="想预测什么事，心念一动，立刻取数，取数可以是心中所想，也可以是看到的比如车牌号、门牌号、电话号码、时间等，要第一反应想到或看到的数。比如想问朋友在不在家，心念一动，恰巧看到手机屏幕上显示的时间是14：36分，就取1436进行测算；"
			>
				<template #reference>
					<el-input placeholder="请输入活数" v-model="state.value" style="width: 425px"> </el-input>
				</template>
			</el-popover>
			<el-button type="primary" style="margin-left: 16px" @click="go">起课</el-button>
		</div>

		<div class="result" v-show="state.cur.title">
			<div class="type">
				{{state.cur.type}}
			</div>

			<div class="title">
				<span>卦象：</span>
				{{ state.cur.title }}
			</div>
			<div class="auther">
				<span>简译：</span>
				{{ state.cur.autherSay }}
			</div>
			<div class="number">
				<span>属相：</span>
				{{ state.cur.number }}
			</div>
			<div class="desc">
				<span>详情：</span>
				{{ state.cur.desc }}
			</div>
		</div>
		<div class="link">
			
			  <el-link type="primary" href="https://github.com/kev1nzh37/ask-god">Github</el-link>
		</div>
	</div>
</template>

<script setup>
import { onMounted, reactive } from "vue"
import { ElMessage } from "element-plus"
const state = reactive({
	value: "",
	cur: { title: "", desc: ``, number: "", autherSay: "" },
	valueObject: [
		{	
			type: '大安',
			title: "[大安] 身不动时，五行属木，颜色青色，方位东方。临青龙，凡谋事主一、五、七。有静止、心安。吉祥之含义。",
			desc: `大安事事昌，求财在坤方，失物去不远，宅舍保安康，行人身未动，病者主无妨。将军回田野，仔细与推详，丢失在附近，可能西南向，安居得吉日，不可动身祥。办事别出屋，求借邀自房，得病凶化吉，久疾得安康，寻人知音信，可能归村庄。口舌能消散，远行要提防，交易别出村，离屯细推详，求财有八分，得全不出房。`,
			number: "身不动时，属木，青龙，凡事主逢一、五、七（寅巳申）",
			autherSay: "吉，持久的，安稳的事情和过程不变。",
		},
		{
			type: '留连',
			title: "[留连] 人未归时，五行属水，颜色黑色，方位北方，临玄武，凡谋事主二、八、十。有喑味不明，延迟。纠缠．拖延、漫长之含义。",
			desc: `留连事未当，求事日莫光，凡事只宜缓，去者未回向，失物南方去，急急行便访。紧记防口舌，人口且平祥，丢失难寻找，窃者又转场，出行定不归，久去拖延长。办事不果断，牵连又返往，求借不易成，被求而彷徨，此日患疾病，几天不复康。找人迷雾中，迷迷又恍惚，口舌继续有，拖拉又伸长，女方嫁吉日，求财六分量。`,
			number: "人未归时，属水，玄武，凡事主逢在二、八、十（卯午子）",
			autherSay: "凶，延迟，拖延，很漫长，曲折，不清不楚。",
		},
		{
			type: '速喜',
			title: "[速喜] 人即至时，五行属火，颜色红色方位南方，临朱雀，谋事主三，六，九。有快速、喜庆，吉利之含义。指时机已到。",
			desc: `速喜喜临乡，求财往南方，失物申午未，逢人路寻详，官事有福德，病者无大伤。六畜田稼庆，行人有音向，丢失得音信，微乐在面上，出行遇吉利，小喜而顺当。办事如逢春，吉利又荣光，小量可求借，大事难全强，久病见小愈，得病速回康，寻人得知见，口舌见消亡，交易可得成，但不太久长，求财有十分，吉时得顺当。`,
			number: "人便至时，属火，朱雀，凡事主在三，六，九 （辰戌未）",
			autherSay: "吉，很快速，喜庆，时机到了",
		},
		{
			type: '赤口',
			title: "[赤口] 官事凶时，五行属金，颜色白色，方位西方，临白虎，谋事主四、七，十。有不吉、惊恐，凶险、口舌是非之含义。",
			desc: `赤口主口伤，官事且紧防，失物急去找，行人有惊慌，鸡犬多作怪，病者上西方。更须防咒咀，恐怕染瘟殃，找物犯谎口，寻问无音向，出门千口怨，言谈万骂伤。办事犯口舌，难成有阻挡，求借不全顺，闭口无事张，得病千口猜，求医还无妨。寻人得凶音，人心不安详，口舌犯最重，交易口舌防，求财只四分，逢吉才成当。`,
			number: "官事凶时，属金，白虎，凡事主在四、七，十",
			autherSay: "凶，口舌之争，官司纠纷。",
		},
		{
			type: '小吉',
			title: "[小吉] 人来喜时，五行属木，临六合，凡谋事主一、五、七有和合、吉利之含义。",
			desc: `小吉最吉昌，路上好商量，阴人来报喜，失物在坤方，行人立刻至，交易甚是强。凡事皆合好，病者保安康，大吉又大顺，万事如意详，出行可得喜，千里吉安祥。诸事可心顺，有忧皆消光，求借自来助，众友愿相帮，重病莫要愁，久病得安康。不见得相见，不打自归庄，千人称赞君，无限上荣光，交易成兴隆，十二分财量.`,
			number: "人来喜时，属水，六合，凡事主逢在一、五、七",
			autherSay: "喜，小惊喜，发小财，不持久。",
		},
		{
			type: '空亡',
			title: "[空亡] 音信稀时，五行属土，颜色黄色，方位中央；临勾陈。谋事主三、六、九。有不吉、无结果、忧虑之含义。",
			desc: `空亡事不长，阴人无主张，求财心白费，行人有灾殃，失物永不见，官事有刑伤。病人遇邪鬼，久病添祸殃，失物难找见，找寻空荡荡，出行不吉利，凶多不吉祥。办事凶为多，处处有阻挡，求借不能成，成事化败伤，得病凶多噩，久患雪加霜。寻人无音信，知音变空想，万口都诽骂，小舟遭狂浪，求财有二分，不吉不利亡`,
			number: "音信稀时，属土，勾陈，凡事主在三、六、九（辰未丑）",
			autherSay: "凶，没有结果，失去核心，没意义。",
		},
	],
})

onMounted(() => {})

const go = () => {
	const { value } = state
	if (!value) {
		ElMessage.warning({
			message: "请输入活数后再起课。",
			type: "warning",
		})
		return
	}

	const valueList = value.split("").map((i) => Number(i))
	const check = !!valueList.filter((i) => isNaN(i)).length

	if (check) {
		ElMessage.warning({
			message: "请输入数字的活数。",
			type: "warning",
		})
		return
	}

	calcResult(valueList)
}
const calcResult = (valueList) => {
	const lenCount = valueList.length === 1 ? 0 : valueList.length - 1
	const sum = valueList.reduce((sumValue, cur) => (sumValue += cur))
	console.log(sum)

	let result = (sum - lenCount) % 6 === 0 ? 5 : ((sum - lenCount) % 6) - 1
	state.cur = state.valueObject[result]
	console.log(sum, lenCount, (sum - lenCount) % 6, result)
}
</script>

<style scoped>
.box {
	width: 800px;
	height: 500px;
	box-shadow: 0 0 6px rgb(0, 0, 0, 0.1);
	padding: 16px;
	position: relative;
}
.box:hover {
	box-shadow: 0 0 12px rgb(0, 0, 0, 0.1);
}
.box > .title {
	text-align: center;
}
.input-wrapper {
	display: flex;
	justify-content: center;
	align-items: center;
	margin: 16px 0;
}
.result {
	margin-top: 50px;
	color: rgba(0, 0, 0, 0.65);
}
.result > div {
	margin-bottom: 24px;
}
.result > div > span {
	color: #5e6d82;
}
.link {
	position: absolute;
	right:16px;
	bottom: 16px;
}
.type {
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 40px;
}
</style>
