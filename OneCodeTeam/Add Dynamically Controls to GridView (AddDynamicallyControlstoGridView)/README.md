# Add Dynamically Controls to GridView (AddDynamicallyControlstoGridView)
## Requires
- Visual Studio 2010
## License
- MS-LPL
## Technologies
- ASP.NET
## Topics
- GridView
## Updated
- 04/20/2012
## Description

<h1>Add Dynamic LinkButton in Gridview(CSASPNETAddDynamicControltoGridView)</h1>
<h2>Introduction </h2>
<p class="MsoNormal">The sample code demonstrates how to add dynamically created controls to the GridView in the CodeBehind page. For some people, when the refresh or the page is PostBack, the dynamically created controls will disappear from GridView, this
 sample will show how to resolve this issue.</p>
<h2>Running the Sample</h2>
<p class="MsoNormal">Please follow these demonstration steps below.</p>
<p class="MsoNormal">Step 1:&nbsp;Open the <span style="">CSASPNETAddDynamicControltoGridView</span>.sln. Expand the
<a name="OLE_LINK1"><span style="">CSASPNETAddDynamicControltoGridView</span> </a>
web application and press Ctrl &#43; F5 to show the Default.aspx. </p>
<p class="MsoNormal">Step 2: We will see a web page like below:</p>
<p class="MsoNormal"><span style=""><img src="56388-image.png" alt="" width="567" height="314" align="middle">
</span></p>
<p class="MsoNormal">Step 3:<span style="">&nbsp; </span>Click on a LinkButton to do a PostBack operations, the page will like show below:</p>
<p class="MsoNormal"><span style=""><img src="56389-image.png" alt="" width="509" height="336" align="middle">
</span></p>
<p class="MsoNormal">Step 4:<span style="">&nbsp;&nbsp; </span>Validation finished.</p>
<h2>Using the Code</h2>
<p class="MsoNormal" style="">Code Logical: <span style="">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></p>
<p class="MsoNormal">Step 1. Create a C# &quot;ASP.NET Web Application&quot; in Visual Studio 2010/Visual Web Developer 2010. Name it as ��<span style="">CSASPNETAddDynamicControltoGridView</span>&quot;.
</p>
<p class="MsoNormal">Step 2.<span style="">&nbsp; </span>Add a GridView Control to ��Default.aspx�� page then rename it to &quot;gdvCustomer&quot;. This page will bind the data and show the dynamically created LinkButton Control. In order to realize this
 page:</p>
<p class="MsoNormal">First, we need to bind data to gdvCustomer<span style="color:black">.
</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>HTML</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">html</span>

<pre id="codePreview" class="html">
&lt;asp:GridView ID=&quot;gdvCustomer&quot; runat=&quot;server&quot; AutoGenerateColumns=&quot;False&quot; OnDataBound=&quot;gdvCustomer_DataBound&quot;
           DataKeyNames=&quot;Id&quot; DataSourceID=&quot;SqlDataSource1&quot;&gt;
           &lt;Columns&gt;
               &lt;asp:TemplateField&gt;
                   &lt;ItemTemplate&gt;
                   &lt;/ItemTemplate&gt;
               &lt;/asp:TemplateField&gt;
               &lt;asp:BoundField DataField=&quot;Id&quot; HeaderText=&quot;Id&quot; InsertVisible=&quot;False&quot; ReadOnly=&quot;True&quot;
                   SortExpression=&quot;Id&quot; /&gt;
               &lt;asp:BoundField DataField=&quot;Name&quot; HeaderText=&quot;Name&quot; SortExpression=&quot;Name&quot; /&gt;
               &lt;asp:BoundField DataField=&quot;Age&quot; HeaderText=&quot;Age&quot; SortExpression=&quot;Age&quot; /&gt;              
           &lt;/Columns&gt;
       &lt;/asp:GridView&gt;
       &lt;asp:SqlDataSource ID=&quot;SqlDataSource1&quot; runat=&quot;server&quot; ConnectionString=&quot;&lt;%$ ConnectionStrings:ConnectionString %&gt;&quot;
           SelectCommand=&quot;SELECT [Id], [Name], [Age] FROM [CustomerInfo]&quot;&gt;&lt;/asp:SqlDataSource&gt;

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><br>
Then, we need to call DataBound method to add dynamically created Control<span style="color:black">.
</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
        protected void gdvCustomer_DataBound(object sender, EventArgs e)
        {
            AddLinkButton();
        }


        /// &lt;summary&gt;
        /// Add a LinkButton To GridView Row.
        /// &lt;/summary&gt;
        private void AddLinkButton()
        {
            foreach (GridViewRow row in gdvCustomer.Rows)
            {
                if (row.RowType == DataControlRowType.DataRow)
                {
                    LinkButton lb = new LinkButton();
                    lb.Text = &quot;Approve&quot;;
                    lb.CommandName = &quot;ApproveVacation&quot;;
                    lb.Command &#43;= LinkButton_Command;
                    row.Cells[0].Controls.Add(lb);
                }
            }
        }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><span style="color:black">To test the LinkButton, we add an event for the LinkButton .
</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void LinkButton_Command(object sender, CommandEventArgs e)
        {
            if (e.CommandName == &quot;ApproveVacation&quot;)
            {
                //This is to test 
                LinkButton lb = (LinkButton)sender;
                lb.Text = &quot;OK&quot;;
            }
        }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><span style="color:black"><br>
<b style="">[Note]</b>Finally, add LinkButton in the Page_Init event and override the OnInit method.</span></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span>
</div>
<span class="hidden">csharp</span>

<pre id="codePreview" class="csharp">
protected void Page_Init(object sender, EventArgs e)
       {
           gdvCustomer.DataBind();
       }


       protected void Page_Load(object sender, EventArgs e)
       {
           if (!IsPostBack)
           {
               AddLinkButton();
           }
       }


       /// &lt;summary&gt;
       /// To initialize the page.
       /// &lt;/summary&gt;
       /// &lt;param name=&quot;e&quot;&gt;&lt;/param&gt;
       protected override void OnInit(EventArgs e)
       {
           base.OnInit(e);
       }

</pre>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p class="MsoNormal"><br>
Step 3. Build the application and you can debug it.</p>
<h2>More Information</h2>
<p class="MsoListParagraph" style="text-indent:-.25in"><span style="font-family:Symbol"><span style="">��<span style="font:7.0pt &quot;Times New Roman&quot;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</span></span></span><a href="http://msdn.microsoft.com/en-us/library/ms178472.aspx">ASP.NET Page Life Cycle Overview</a></p>
<hr>
<div><a href="http://go.microsoft.com/?linkid=9759640" style="margin-top:3px"><img alt="" src="http://bit.ly/onecodelogo">
</a></div>
