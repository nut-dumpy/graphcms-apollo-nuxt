<template>
	<h2 v-if="loading > 0">
      Loading...
    </h2>
    <div v-else>
      <article>
        <h1>{{survey.name}}</h1>
		<ul>
			<li v-for="field in survey.fields" key="field.name">
				<span v-if="field.type !== 'label'">
					<label :for="field.name">{{field.name}}</label>
					<input :type="field.type" :id="field.name" :placeholder="field.name"/>
				</span>
				<span v-else class="label">
					<label>{{field.name}}</label>
				</span>
			</li>
		</ul>
      </article>
    </div>
</template>

<script>
  import gql from 'graphql-tag'

  const survey = gql`
    query survey($name: String!) {
      survey: Survey(name: $name) {
        name
        fields
        organization {
           name
        }
      }
    }
  `

export default {
    name: 'Survey',
    data: () => ({
      loading: 0
    }),
    apollo: {
      $loadingKey: 'loading',
      survey: {
        query: survey,
        variables () {
          return { name: this.$route.params.name }
        }
      }
    }
  }
</script>

<style scoped>
li {

		list-style: none;
}
li span {
	display: flex;
	justify-content: space-between;
	margin-bottom: 8px;
}
li span > * {
	flex-basis: 12em;
}
li span.label > * {
	color: #888;
	flex-basis: 100%;
}
</style>
