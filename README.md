# Live-Project-Contributions

<h3>Introduction</h3>

<hr>

<p>My first foray into collaborative software development took place 
during my time at The Tech Academy when they had me work with my 
fellow students on a full scale MVC application in C#.  Not only was 
it a great opportunity to add features and fix bugs, but it was
also helpful in incrasing my confidence by teaching me that I am 
capable of this sort of work and in introducing me to software 
development on a professional level.

The two week sprint allowed each student to work on both front and 
back end stories for an employee management website for a construction
company.  During the week we would have daily standup meetings and
at the end of each week we would have a sprint retrospective. Due to 
my own personal time constraints, I focused a bit more on 
<a href="#front-end-stories">front end</a> stories though I did complete 
one <a href="#back-end-stories">back end</a> story that I am proud of.

Below are descriptions for the stories that I worked on, some before
and after photos of the front end stories, as well as some code
snippets for the back end story that I completed.
</p>

<hr>

<a id="user-content-front-end-stories" class="anchor" aria-hidden="true" href="#front-end-stories"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
<h3>Front End Stories</h3>

<hr>

<h4>New User Button Alignment</h4>

<p>I aligned the buttons on the new user page so they show as a row instead of 
 a column. I also, made a small aesthetic change to one of the input labels.</p>
 
<h4>Before:</h4>
 
![B4Buttons](https://user-images.githubusercontent.com/46905735/68080356-0d919d00-fdb7-11e9-81c9-342047248935.png)
 
<h4>After:</h4>

![AfterButtons](https://user-images.githubusercontent.com/46905735/68080376-809b1380-fdb7-11e9-88cd-0e0db1b33e93.png)



<h4>Homepage Realignment</h4>

<p>I made the home page jumbotron more aesthetically pleasing by having it align with the buttons on the bottom of the page</p>

<h4>Before:</h4>

![B4Homepage](https://user-images.githubusercontent.com/46905735/68080379-84c73100-fdb7-11e9-91a4-6698c1741b88.png)

<h4>After:</h4>

![AfterHomepage](https://user-images.githubusercontent.com/46905735/68080384-9577a700-fdb7-11e9-9c84-cb4ea271debd.png)



<h4>Details Page Update</h4>

<p>The page detailing information for a specific job was pretty all over the place so I combined everything in one simple, more 
 elegant format</p>
 
<h4>Before:</h4>
 
![B4Combine](https://user-images.githubusercontent.com/46905735/68080396-bcce7400-fdb7-11e9-9c99-3a4a46822e52.png)
 
 <h4>After:</h4>
 
![AfterCombine](https://user-images.githubusercontent.com/46905735/68080434-5b5ad500-fdb8-11e9-8faa-e2b9d0ac4d13.png)



<a id="user-content-back-end-stories" class="anchor" aria-hidden="true" href="#back-end-stories"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
<h3>Front End Stories</h3>

<hr>

<h4>User View Update</h4>

<p>The original code made it so that no matter who was logged in, that user saw the same saw information as everyone else.  I updated this by creating a new view for those who were not an admin for the site.  The following will show the code snippets I used as well as what each user saw.</p>

<h4>Original Schedule View (became view for only the Admin user):</h4>

![B4Filter](https://user-images.githubusercontent.com/46905735/68101468-a50ff200-fe82-11e9-82f4-7ee3b85dbca9.png)

<h4>Code For Non-Admin Partial View:</h4>
<pre><code>
@using ManagementPortal.Helpers
@using ManagementPortal.Enums


@model ManagementPortal.ViewModels.MySchedulesVM

@if (Model.hasJobs)
{
    <div class="card card-shadow mb-3">
        <div class="card-header">
            <h4>Managing</h4>
        </div>
        <div class="card-body">
            @if (Model.managedJobs.Count > 0)
            {
                <table class="table w-100">
                    <tr>
                        <th>Title</th>
                        <th>Job Type</th>
                        <th>Location</th>
                        <th>Start Date</th>
                        <th>End Date</th>
                        <th>Notes</th>
                        <th>&nbsp;</th>
                    </tr>
                    @foreach (var job in Model.managedJobs)
                    {
                    <tr>
                        <td> @Html.DisplayFor(m => job.JobTitle) </td>
                        <td> @Html.DisplayFor(m => job.JobType) </td>
                        <td> @Html.DisplayFor(m => job.Location.SiteName) </td>
                        @foreach (var schedule in job.Schedules)
                        {
                            <td> @Html.DisplayFor(m => schedule.StartDate) </td>
                            <td> @Html.DisplayFor(m => schedule.EndDate) </td>
                        }
                        <td> @Html.DisplayFor(m => job.Details.Note) </td>

                        <td class="text-right">
                            @Html.AnchorButton(AnchorType.Details, Url.Action("Details", "Jobs", new { id = job.JobIb }))
                            @Html.AnchorButton(AnchorType.Edit, Url.Action("Edit", "Jobs", new { id = job.JobIb }))
                            @Html.AnchorButton(AnchorType.Delete, Url.Action("Delete", "Jobs", new { id = job.JobIb }))
                        </td>
                    </tr>
                    }
                </table>
            }
            else
            {
                <p>You are not currently managing any jobs.</p>
            }
        </div>
    </div>

    <div class="card card-shadow">
        <div class="card-header">
            <h4>Working</h4>
        </div>
        <div class="card-body">
            @if (Model.scheduledOnJobs.Count > 0)
            {
                <table class="table w-100">
                    <tr>
                        <th>Title</th>
                        <th>Type</th>
                        <th>Location</th>
                        <th>Start Date</th>
                        <th>End Date</th>
                        <th>Notes</th>
                        <th>&nbsp;</th>
                    </tr>
                    @foreach (var schedule in Model.scheduledOnJobs)
                    {
                    <tr>
                        <td>@Html.DisplayFor(m => schedule.Job.JobTitle)</td>
                        <td>@Html.DisplayFor(m => schedule.Job.JobType)</td>
                        <td>@Html.DisplayFor(m => schedule.Job.Location.SiteName)</td>
                        <td>@Html.DisplayFor(m => schedule.StartDate)</td>
                        <td>@Html.DisplayFor(m => schedule.EndDate)</td>
                        <td>@Html.DisplayFor(m => schedule.Job.Details.Note)</td>
                        <td class="text-right">
                            @Html.AnchorButton(AnchorType.Details, Url.Action("Details", "Jobs", new { id = schedule.Job.JobIb }))
                        </td>
                    </tr>
                    }
                </table>
            }
            else
            {
                <p>You are not currently scheduled for any jobs.</p>
            }
        </div>
    </div>
}
else
{
    <p>You must be logged in to see jobs.</p>
}
</code></pre>

<h4>Code Snippet On Dashboard View Which Determined Which View The User Would See:</h4>

<pre><code>
<div class="card-body" id="cardbodyBackground">

    @*separates views depending on user.*@

    @if (User.IsInRole("Admin"))
    {
        <div class="card-header">
            <h3 class="text-white">Active Jobs</h3>
        </div>
        Html.RenderAction("_Schedules", "Schedules");
    }
    else
    {
        { Html.RenderAction("_MySchedule", "Schedules"); }
    }
</div>
</code></pre>

<h4>Code Snippet Of Controller Change Which Allowed View Update To Function Properly:</h4>

<pre><code>
[ChildActionOnly]
public ActionResult _MySchedule()
{
    // initialize a view model. the VM has a default false value for hasJobs.
    var viewModel = new MySchedulesVM();

    // get the currently logged in userId, and then find the jobs associated with the use.
    // pass them into a view model, and ultimately the partial view
    var userId = User.Identity.GetUserId();

    // try/catch for null values in Schedule.EndDate and other possibilities.
    try
    {
        if (userId != null)
        {
            viewModel.hasJobs = true;
            viewModel.managedJobs = db.Jobs.Include(jd => jd.Details).Where(j => j.Manager.Id == userId).ToList();
            viewModel.scheduledOnJobs = db.Schedules.Include(s => s.Job.Details).Where(s => s.Person.Id == userId).Where(s =>                       s.Job.Active == true).ToList();
        }

        return PartialView("_MySchedule", viewModel);
    }
    catch (Exception ex)
    {
        return View("Error");
    }            
}
</code></pre>

<h4>Non-Admin User View:</h4>

![AfterFilter](https://user-images.githubusercontent.com/46905735/68101718-e6ed6800-fe83-11e9-9e6c-2c3f907c4602.png)
 
 
