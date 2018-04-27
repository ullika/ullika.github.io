<html>
<head></head>
<body>
<h1>Welcome to labtime!</h1>
<p>Here you can get an overview of all your commits during a specified time.</p>
<p>Please enter your project data in json format.
	example:   {"id":6,"branches":{"master"}},{"id":149,"branches":{"master"}},{{"id":146,"branches":{"dev","master"}} <br>
	You can filter by specific user names. Enter them as json, too!
</p>
<p>
	You have to get yourself a gitlab access token from your personal settings on your gitlab account!
</p>
<form id="data-form">
	<table>
		<tr>
			<td><label for="access-token-field">Access token</label></td>
			<td> <input id="access-token-field"></td>
		</tr>
		<tr>
			<td><label for="user-name-field">User filter</label></td>
			<td><input id="user-name-field"></td>
		</tr>
		<tr>
			<td><label for="project-id-field">Projects</label></td>
			<td><input id="project-id-field"></td>
		</tr>
		<tr><td>
				<button id="add-id-button">Add</button>
				<button id="reset-ids-button">Reset</button>
			</td>
		</tr>

	</table>


	<table>
		<tr>
			<td>
				<h4>Ids</h4>
			</td>
			<td>
				<div id="id-div"></div>
			</td>
		</tr>

	</table>
	<div>
		<label for="start-datepicker">Start</label>
		<input id="start-datepicker">
	</div>
</form>
<button id="get-button">Get!</button>
<div>
	<h4>Result</h4>
	<div id="result-div"></div>
</div>

<script src="http://code.jquery.com/jquery-latest.min.js"></script>
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
<script src="http://stevenlevithan.com/assets/misc/date.format.js"></script>
<script>
    $(document).ready(function () {
        let configuration = '[{"name":"base","id":6,"branches":["master"]},{"name":"dgpraec","id":149,"branches":["master"]},{"name":"yoger","id":146,"branches":["dev","master"]},{"name":"sweetparadise","id":83,"branches":["master","release","experimental","releasetest","phillipp_stash"]}]';
        let panel = $("#result-div");
        let id_list = $("#id-div");
        $("#start-datepicker").datepicker({dateFormat: "yy-mm-ddT00:00:00Z"}).val("2018-03-01T00:00:00Z");
        $("#project-id-field").val(configuration);
        $("#user-name-field").val('["ullika"]');

        //for adding new project ids
        let projects = [];
        $("#add-id-button").click(function () {
            projects = JSON.parse($("#project-id-field").val());
            id_list.html(JSON.stringify(projects));
            return false; //to prevent form submission
        });

        $("#reset-ids-button").click(function () {
            projects = [];
            $("#id-div").html(projects);
            return false; //to prevent form submission
        });

        function get_name(id) {
            for (let i = 0; i < projects.length; i++) {
                let obj = projects[i];
                if (obj["id"] === id) {
                    return ((typeof obj["name"]) !== "undefined") ? obj["name"] : id;
                }
            }
            return "id not found";
        }

        function sort_by_date(commits) {
            return commits.sort(function (a, b) {
                a_date = new Date(a["committed_date"]);
                b_date = new Date(b["committed_date"]);
                return a_date - b_date;
            })
        }

        function remove_double_entries(sorted_commits) {
            cleaned = [];
            sorted_commits.forEach(function (obj) {
                if (typeof last_id !== "undefined" && last_id === obj["short_id"]) {
                    last_obj = cleaned.pop();
                    last_obj["ref_name"] += ", " + obj.ref_name;
                    cleaned.push(last_obj);
                } else {
                    last_id = obj["short_id"];
                    cleaned.push(obj);
                }
            });

            return cleaned;
        }

        function print_table(commits, user_names) {
            console.log("print table");
            console.log("commits: " + JSON.stringify(commits));
            let classes = ["background1", "background2"];
            let current_class = 0;
            let ans = "<table><tr><th>date</th><th>project</th><th>name</th><th>branch</th><th>title</th></tr>";
            let daystart;
            let current;
            let last;
            let firstentry = true;
            for (let i = 0; i < commits.length; i++) {

                let obj = commits[i];
                if (user_names.length > 0 && !user_names.includes(obj["committer_name"])) {
                    continue;
                }
                if (firstentry) {
                    daystart = last = new Date(obj["committed_date"]);
                }

                current = new Date(obj["committed_date"]);
                if (current.toDateString() !== last.toDateString()) {
                    let time_diff = last.getTime() - daystart.getTime();
                    let hours = Math.floor(time_diff / (1000 * 3600));
                    let minutes = Math.floor((time_diff - hours * 1000 * 3600) / (1000 * 60));
                    current_class = (current_class + 1) % 2;
                    ans += "<tr class='background3'><td>working hours:" + daystart.format("HH:MM") + "-" + last.format("HH:MM");
                    if (time_diff > 0) {
                        ans += " time: " + hours + " hours and " + minutes + " minutes."
                    }
                    ans += "</td></tr>";
                    daystart = current;
                }
                ans +=
                    "<tr class='" + classes[current_class] + "'>" +
                    "<td>" + dateFormat(current) + "</td>" +

                    "<td>" + get_name(obj["project"]) + "</td>" +
                    "<td>" + obj["committer_name"] + "</td>" +
                    "<td>" + obj["ref_name"] + "</td>" +
                    "<td>" + obj["title"] + "</td>" +
                    "</tr>";
                firstentry = false;
                last = current;
            }

            return ans + "</table>";
        }


        //for submitting to the api
        function request_project_commits(id, ref_name, start, page_offset,token) {
            let settings = {
                "async": false,
                "crossDomain": true,
                "url": "https://gitlab.codel1.de/api/v4/projects/" + id + "/repository/commits",
                "method": "GET",
                "data": {"page": page_offset, "since": start, "ref_name": ref_name},
                "headers": {
                    "PRIVATE-TOKEN": token                }
            };
            let promise = $.ajax(settings);
            let commits = JSON.parse(promise.responseText);
            let my_commits = [];
            commits.forEach(function (obj, index, commits) {


                obj["ref_name"] = ref_name;
                obj["project"] = id;

                my_commits.push(obj);

            });
            return my_commits;
        }

        $("#get-button").click(function () {
            let start = $("#start-datepicker").val();
            let user_filter = $("#user-name-field").val();
            let token=$("#access-token-field").val();
            let commits = [];

            projects.forEach(function (project) {
                ref_names = project["branches"];
                ref_names.forEach(function (ref_name) {
                    let page = 1;
                    do {
                        recent = request_project_commits(project["id"], ref_name, start, page, token);
                        commits = commits.concat(recent);
                        page++;
                    } while (recent.length > 0);
                });
            });
            console.log("before sorting");
            sorted = sort_by_date(commits);
            cleaned = remove_double_entries(sorted);
            panel.html(print_table(cleaned, user_filter));
        });
    })
</script>

<style>
	.background1 {
		background-color: lightgray;
	}

	.background2 {
		background-color: khaki;
	}

	.background3 {
		background-color: white;
	}
</style>
</body>
</html>