# RoverCore Datatables

This small library provides extension methods that allow CRUD index pages to easily generate the data necessary for server-side Datatables.


## Usage

### Install

Install the package using NuGet  
`Install-Package RoverCore.Datatables`

Show below is a controller action method that generates the JSON necessary to power server-side Datatables.  The returned view data is determined by a ViewModel and can be searched, sorted, and paged.

```
        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<IActionResult> GetRoles(DtRequest request)
        {
            try
            {
                var jsonData = await _context.Roles.GetDatatableResponseAsync<ApplicationRole, ApplicationRoleIndexViewModel>(request);

                return Ok(jsonData);
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Error generating Roles index json");
            }

            return StatusCode(500);
        }
```