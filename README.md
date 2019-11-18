# Live-Project-Contributions

<h3>Introduction</h3>

<hr>

<p>My first foray into collaborative software development took place during my time at The Tech Academy when they had me work with my fellow students on a full scale MVC application in C#.  Not only was it a great opportunity to add features and fix bugs, but it was
also helpful in increasing my confidence by teaching me that I am capable of this sort of work and in introducing me to software development on a professional level.

The two week sprint allowed each student to work on both front and back end stories for an employee management website for a construction company.  During the week we would have daily standup meetings and at the end of each week we would have a sprint retrospective.  Due to my own personal time constraints, I focused a bit more on <a href="#front-end-stories">front end</a> stories though I did complete one <a href="#back-end-stories">back end</a> story that I am proud of.

Below are descriptions for the stories that I worked on, some before and after photos of the front end stories, as well as some code
snippets for the back end story that I completed.
</p>

<hr>

<a id="user-content-front-end-stories" class="anchor" aria-hidden="true" href="#front-end-stories"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
<h3>Front End Stories</h3>

<hr>

<h4>New User Button Alignment</h4>

<p>I aligned the buttons on the new user page so they show as a row instead of a column. I also, made a small aesthetic change to one of the input labels.</p>
 
<h4>Before:</h4>
 
![B4Buttons](https://user-images.githubusercontent.com/46905735/68080356-0d919d00-fdb7-11e9-81c9-342047248935.png)
 
<h4>After:</h4>

![AfterButtons](https://user-images.githubusercontent.com/46905735/68080376-809b1380-fdb7-11e9-88cd-0e0db1b33e93.png)



<h4>Homepage Realignment</h4>

<p>I made the home page jumbotron more aesthetically pleasing by having it align with the buttons on the bottom of the page.</p>

<h4>Before:</h4>

![B4Homepage](https://user-images.githubusercontent.com/46905735/68080379-84c73100-fdb7-11e9-91a4-6698c1741b88.png)

<h4>After:</h4>

![AfterHomepage](https://user-images.githubusercontent.com/46905735/68080384-9577a700-fdb7-11e9-9c84-cb4ea271debd.png)



<h4>Details Page Update</h4>

<p>The page detailing information for a specific job was pretty all over the place so I combined everything in one simple, more 
 elegant format.</p>
 
<h4>Before:</h4>
 
![B4Combine](https://user-images.githubusercontent.com/46905735/68080396-bcce7400-fdb7-11e9-9c99-3a4a46822e52.png)
 
 <h4>After:</h4>
 
![AfterCombine](https://user-images.githubusercontent.com/46905735/68080434-5b5ad500-fdb8-11e9-8faa-e2b9d0ac4d13.png)



<a id="user-content-back-end-stories" class="anchor" aria-hidden="true" href="#back-end-stories"><svg class="octicon octicon-link" viewBox="0 0 16 16" version="1.1" width="16" height="16" aria-hidden="true"><path fill-rule="evenodd" d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"></path></svg></a>
<h3>Back End Stories</h3>

<hr>

<h4>User View Filter</h4>

<p>The original code made it so that no matter who was logged in, that user saw the same information as everyone else.  I updated this by creating a new view for those who were not an admin for the site.  The following images and code snippets shows the updates that I made:</p>

<h4>Original Schedule View (became view for only the admin user):</h4>

![B4Filter](https://user-images.githubusercontent.com/46905735/68101468-a50ff200-fe82-11e9-82f4-7ee3b85dbca9.png)

<h4>New View For Non-Admin User:</h4>

![AfterFilter](https://user-images.githubusercontent.com/46905735/68101718-e6ed6800-fe83-11e9-9e6c-2c3f907c4602.png)

<p>The following is the code snippet found on the Dashboard View that determined which user was making the information request:</p>

<pre>
<code>
        @*separates views depending on user.*@

        @if (User.IsInRole("Admin"))
        {
            Html.RenderAction("_Schedules", "Schedules");
        }
        else
        {
            { Html.RenderAction("_MySchedule", "Schedules"); }
        }
</code>
</pre>

<p>The following is a code snippet for how the Schedule Controller handled the whole user filter:</p>

<pre>
<code>
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
</code>
</pre>

<h4>Job Creation Filters</h4>

<p>The job creation page had some issues in that there were multiple optional parameters that did not allow for null values (including the application crashing if no shift time was input), and the manager drop down menu held employees that were neither a manager nor an administrator.  I updated all of these aspects in the following code snippets:</p>

<pre>
<code>
     //Commented out the "required" property as it causes the ModelState to become false if a null value is
     //entered into the Weekly Shifts portion of the Create Job form.
     //[Required] 
     [MaxLength(100)]
     [StringLength(100, MinimumLength = 1, ErrorMessage = "Please enter a default shift time.")]
     [Display(Name = "Default")]
     public string Default { get; set; }

</code>
</pre>

<pre>
<code>
     private void PopulateJobDropDowns(object model, int JobId = 1, string UserId = null)
     {
         List<SelectListItem> jobSites = new SelectList(db.JobSites, "JobSiteID", "SiteName", JobId).ToList();
         //Adds null choice in drop down menu.
         jobSites.Insert(0, (new SelectListItem { Text = "--None--", Value = "0" }));
         ViewData["JobSites"] = jobSites;

         List<SelectListItem> users;
         if (UserId == null)
         {
             //filters drop downs to only include Managers and Admins who are not suspended.
             users = new SelectList(from c in db.Users
                                    where (c.UserRole == "Manager" || c.UserRole == "Admin") && c.Suspended == false
                                    select c, "Id", "FullName").ToList();
             //Adds null choice in drop down menu.
             users.Insert(0, (new SelectListItem { Text = "--None--", Value = "0" }));
         }
         else
         {
             //filters drop downs to only include Managers and Admins who are not suspended.
             users = new SelectList(from c in db.Users
                                    where (c.UserRole == "Manager" || c.UserRole == "Admin") && c.Suspended == false
                                    select c, "Id", "FullName").ToList();
             //Adds null choice in drop down menu.
             users.Insert(0, (new SelectListItem { Text = "--None--", Value = "0" }));
         }
         ViewData["Users"] = users;
     }
</code>
</pre>

<h3>Summary</h3>

<hr>

<p>Overall, my Live Project at The Tech Academy was a fantastic and invaluable experience which gave me the confidence and skills to succeed in my future endeavors as a Junior Software Developer!</p>
