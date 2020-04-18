
https://spring.io/guides/gs/rest-service/

## Controller
```
@RestController
@RequestMapping("/v1/projects")
@Api(value = "project", description = "A project represents a user-defined group of related files, directories, and other projects.")
public class Project {

	private static final Logger logger = LogManager.getLogger(Project.class);
	
	@Autowired
	private ProjectService projectService;
	
	@ApiOperation(value="show all Projects")
    @RequestMapping(method = RequestMethod.GET, produces = "application/json")
    public List<ProjectDetails> showProjects() throws IOException, InterruptedException {
 	return projectService.showProject();
	}
	
	@ApiOperation(value="creates a project")
	@RequestMapping(method = RequestMethod.POST, produces = "application/json")
	public ResponseEntity<ResponseDto> createProject(@RequestBody ProjectDto details) throws IOException, InterruptedException {
		return projectService.createProject(details);
	}
	
	@ApiOperation(value="Retrieves all the versions of a project or directory.")
	@RequestMapping(value="/{projectName}", method = RequestMethod.GET, produces = "application/json")
	public List<ProjectVersion> findProject(@PathVariable String projectName) throws IOException, InterruptedException {
		return projectService.findProject(projectName);
	}
	
	@ApiOperation(value="Updates the Project and its Subprojects.")
	@RequestMapping(value="/{projectName}/update", method = RequestMethod.POST, produces = "application/json")
	public ResponseEntity<ResponseDto> updateProject(@PathVariable String projectName) throws IOException, InterruptedException {
		return projectService.updateProject(projectName);
	}
	
	@ApiOperation(value="Returns the work area path of a project.")
	@RequestMapping(value="/path/{projectSpec}", method = RequestMethod.GET, produces = "application/json")
	public ResponseEntity<Object> findProjectPath(@PathVariable String projectSpec) throws IOException, InterruptedException {
		return projectService.findProjectPath(projectSpec);
	}
	
	@ApiOperation(value="Compares between two objects.")
	@RequestMapping(value="/compare", method = RequestMethod.GET, produces = "application/json")
	public ResponseEntity<ResponseDto> compareObject(@RequestParam String object1,@RequestParam String object2) throws IOException, InterruptedException {
		logger.debug("Passed paramerters are "+object1+" "+object2);
		return projectService.compareObject(object1,object2);
	}
	
/*	@ApiOperation(value="Finds a project by its version")
	@RequestMapping(value="/{projectName}/{version}", method = RequestMethod.GET, produces = "application/json")
	public ResponseDto findProjectByVersion(@PathVariable String projectName,@PathVariable String version) throws IOException, InterruptedException {
		return projectService.findProjectByVersion(projectName,version);
	}*/
		
	@ApiOperation(value="Creates a modifiable version of a project.")
	@RequestMapping(value="/copy-project",method = RequestMethod.POST,produces = "application/json")
	public ResponseEntity<ResponseDto> copyProject(@RequestBody CopyProject details) throws IOException, InterruptedException {		
		return projectService.copyProject(details);
	}
	
	/*@ApiOperation(value="adds file to the specified project.")
	@RequestMapping(value="/files",method = RequestMethod.POST)
	public ResponseEntity<ResponseDto> addFiles(@RequestBody FileDto details) throws IOException, InterruptedException {
		return projectService.addFiles(details);
	}*/
	
	@ApiOperation(value="Checks in an object.")
	@RequestMapping(value="/files/{fileName}/checkin",method = RequestMethod.POST)
	public ResponseEntity<ResponseDto> checkinFiles(@PathVariable String fileName,@RequestBody CheckIn details) throws IOException, InterruptedException {
		return projectService.checkinFiles(fileName,details);
	}
	
	@ApiOperation(value="Checks out an object.")
	@RequestMapping(value="/files/{fileName}/checkout",method = RequestMethod.POST)
	public ResponseEntity<ResponseDto> checkoutFiles(@PathVariable String fileName,@RequestBody CheckOut details) throws IOException, InterruptedException {
		return projectService.checkoutFiles(fileName,details);
	}
	
	@ApiOperation(value="Checks in a project.")
	@RequestMapping(value="{projectSpec}/checkin",method = RequestMethod.POST)
	public ResponseEntity<ResponseDto> checkinProject(@PathVariable String projectSpec,@RequestBody CheckIn details) throws IOException, InterruptedException {
		return projectService.checkinFiles(projectSpec,details);
	}	
	
	@ApiOperation(value="Tracks all the uncontrolled files.")
	@RequestMapping(value="{projectSpec}/track", method = RequestMethod.GET, produces = "application/json")
	public List<TrackFiles> findUncontrolledFiles(@PathVariable String projectSpec) throws IOException, InterruptedException {
		return projectService.findUncontrolledFiles(projectSpec);
	}
	
	@ApiOperation(value="Adds all the uncontrolled files.")
	@RequestMapping(value="/track", method = RequestMethod.POST, produces = "application/json")
	public ResponseEntity<ResponseDto> addUncontrolledFiles(@RequestBody TrackDto trackDto) throws IOException, InterruptedException {
		return projectService.addUncontrolledFiles(trackDto);
	}
	
	@ApiOperation(value="Synchronize the Work Area of Project")
	@RequestMapping(value="{projectName}/sync", method = RequestMethod.POST, produces = "application/json")
	public ResponseEntity<ResponseDto> syncWorkAreaOfProject(@PathVariable String projectName) throws IOException, InterruptedException {
		return projectService.syncWorkAreaOfProject(projectName);
	}
	
}
```

##	Service
```
@Service
public class ProjectService {

	private static final Logger logger = LogManager.getLogger(ProjectService.class);
	@Autowired
	private ProcessUtility processUtility;

	@Autowired
	private PathDTO pathDto;

	List<String> msg = new ArrayList<String>();

	public List<ProjectDetails> showProject() throws IOException, InterruptedException {
		Process p = Runtime.getRuntime()
				.exec(new String[] { "ccm", "show", "-p", "-f", "%name:%status:%owner:%cvtype:%task", "-u" });
		ResponseEntity<ResponseDto> res = processUtility.executeProcess(p);
		int statusCode = res.getStatusCodeValue();
		if (statusCode == 200) {
			int size = res.getBody().getMessage().size() - 1;
			ArrayList<String> al = new ArrayList<String>();
			String name, status, owner, cvType, task;
			List<ProjectDetails> pDetails = new ArrayList<ProjectDetails>();

			for (int i = 0; i <= size; i++) {
				String[] values = res.getBody().getMessage().get(i).trim().split(":");
				for (String val : values) {
					al.add(val);
				}
			}

			logger.debug("Size " + al.size());
			for (int s = 0; s < al.size(); s += 5) {
				name = al.get(s);
				status = al.get(s + 1);
				owner = al.get(s + 2);
				cvType = al.get(s + 3);
				task = al.get(s + 4);
				pDetails.add(new ProjectDetails(name, status, owner, cvType, task));
			}

			for (ProjectDetails s : pDetails) {
				logger.debug(s.getName() + " " + s.getOwner() + " " + s.getStatus() + " " + s.getCvtype() + " "
						+ s.getTask());
			}
			return pDetails;
		} else {
			throw new DataNotFoundException("Response Error.Please try again.");
		}

	}

	public ResponseEntity<ResponseDto> createProject(ProjectDto projectdto) throws IOException, InterruptedException {
		String projName = projectdto.getProjectName();
		String purpose = projectdto.getPurpose();
		String taskID = projectdto.getTask();
		Process p = Runtime.getRuntime().exec(
				new String[] { "ccm", "create", "-t", "project", "-purp", purpose, "-cb", "-task", taskID, projName });
		return processUtility.executeProcess(p);
	}

	/*
	 * public ResponseDto findProjectByVersion(String projName,String version)
	 * throws IOException, InterruptedException { Process p=
	 * Runtime.getRuntime().exec(new String[] {"ccm","query","-name", projName,
	 * "-v", version}); return processUtility.executeProcess(p); }
	 */

	public ResponseEntity<ResponseDto> updateProject(String projectName) throws IOException, InterruptedException {
		logger.debug("Updating Project:" + projectName);
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "update", "-rs", "-p", projectName });
		return processUtility.executeProcess(p);
	}

	public List<ProjectVersion> findProject(String objectName) throws IOException, InterruptedException {
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "query", "-name", objectName, "-f",
				"%displayname,%status,%owner,%cvtype,%project,%task", "-u" });
		ResponseEntity<ResponseDto> res = processUtility.executeProcess(p);
		int statusCode = res.getStatusCodeValue();
		if (statusCode == 200) {
			int size = res.getBody().getMessage().size() - 1;
			ArrayList<String> al = new ArrayList<String>();
			String displayname, status, owner, cvType, project, task;
			List<ProjectVersion> pVersion = new ArrayList<ProjectVersion>();

			for (int i = 0; i <= size; i++) {
				String[] values = res.getBody().getMessage().get(i).trim().split(",");
				for (String val : values) {
					al.add(val);
				}
			}

			logger.debug("Size " + al.size());
			for (int s = 0; s < al.size(); s += 6) {
				displayname = al.get(s);
				status = al.get(s + 1);
				owner = al.get(s + 2);
				cvType = al.get(s + 3);
				project = al.get(s + 4);
				task = al.get(s + 5);

				pVersion.add(new ProjectVersion(displayname, status, owner, cvType, project, task));
			}

			for (ProjectVersion s : pVersion) {
				logger.debug(s.getDisplayname() + " " + s.getOwner() + " " + s.getStatus() + " " + s.getCvtype() + " "
						+ s.getTask());
			}
			return pVersion;
		} else {
			throw new DataNotFoundException("Project Not found");
		}

	}

	public ResponseEntity<ResponseDto> copyProject(CopyProject copyproject) throws IOException, InterruptedException {
		String projectSpec = copyproject.getProjectSpec();
		String purpose = copyproject.getPurpose();
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "cp", "-purpose", purpose, projectSpec });
		return processUtility.executeProcess(p);
	}

	/*
	 * public ResponseEntity<ResponseDto> addFiles(FileDto details) throws
	 * IOException, InterruptedException { String type = details.getFileType();
	 * String fileName = details.getFilePath(); // give
	 * /home/ccm_root/ccm_wa/InformixDB/Operation-1/Operation/Hello.java absolute
	 * path String taskId = details.getTaskId(); Process p=
	 * Runtime.getRuntime().exec(new String[] {"ccm","create","-type",
	 * type,fileName,"-task",taskId}); return processUtility.executeProcess(p); }
	 */

// same for files/directory
	public ResponseEntity<ResponseDto> checkinFiles(String name, CheckIn details)
			throws IOException, InterruptedException {
		String userHome = System.getProperty("user.home");
//		String projectPath = userHome+"/ccm_wa/InformixDB/"+projectSpec;
		String path = userHome + "/" + details.getPath();
		String state = details.getState();
		String comment = details.getComment();
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "ci", "-c", comment, "-s", state, path });
		return processUtility.executeProcess(p);
	}

	public ResponseEntity<ResponseDto> checkoutFiles(String name, CheckOut details)
			throws IOException, InterruptedException {
		String userHome = System.getProperty("user.home");
		String filePath = userHome + "/" + details.getDirPath();
		String taskid = details.getTaskid();
		String comment = details.getComment();
		String version = details.getVersion();
		Process p = Runtime.getRuntime()
				.exec(new String[] { "ccm", "co", "-c", comment, "-task", taskid, filePath, "-t", version });
		return processUtility.executeProcess(p);
	}

	public ResponseEntity<Object> findProjectPath(String projectSpec) throws IOException, InterruptedException {
		String userHome = System.getProperty("user.home");
		Process p = Runtime.getRuntime()
				.exec(new String[] { "ccm", "wa", "-show", projectSpec, "-nch", "-f", "%displayname,%wa_path" });
		ResponseEntity<ResponseDto> res = processUtility.executeProcess(p);
		int statusCode = res.getStatusCodeValue();
		if (statusCode == 200) {
			String[] msg = res.getBody().getMessage().get(0).trim().split(",");
			pathDto.setProject(msg[0]);
			// String[] relativePath = msg[1].split("/",4);
			// logger.debug("The relative Path is :: "+
			// relativePath[relativePath.length-1]);
			// pathDto.setWork_Area_Path(msg[1]);
			Path pathAbsolute = Paths.get(msg[1]);
			Path pathBase = Paths.get(userHome);
			Path pathRelative = pathBase.relativize(pathAbsolute);
			pathDto.setWork_Area_Path(pathRelative.toString());

			return new ResponseEntity<>(pathDto, HttpStatus.valueOf(statusCode));
		} else {
			return new ResponseEntity<>(res, HttpStatus.valueOf(statusCode));
		}
	}

	/*
	 * public ResponseEntity<ResponseDto> compareProject(String projectName1, String
	 * projectName2) throws IOException, InterruptedException { Process p=
	 * Runtime.getRuntime().exec(new String[]
	 * {"ccm","diff","-vc","-p",projectName1,projectName2}); return
	 * processUtility.executeProcess(p); }
	 */

	public ResponseEntity<ResponseDto> compareObject(String obj1, String obj2)
			throws IOException, InterruptedException {
		String userHome = System.getProperty("user.home");
		obj1 = userHome + "/" + obj1;
		obj2 = userHome + "/" + obj2;
		logger.debug("Main API :: Compare Object..." + obj1 + " " + obj2);
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "diff", "-vc", obj1, obj2, });
		return processUtility.executeProcess(p);
	}

	public List<TrackFiles> findUncontrolledFiles(String projectName) throws IOException, InterruptedException {
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "reconcile", "-p", projectName, "-no_recurse",
				"-consider_uncontrolled", "-f", "%path,%conflict_message", "-nch" });
		ResponseEntity<ResponseDto> res = processUtility.executeProcess(p);
		int statusCode = res.getStatusCodeValue();
		if (statusCode == 200) {
			int size = res.getBody().getMessage().size() - 1;
			ArrayList<String> al = new ArrayList<String>();
			String path, conflict_message;
			List<TrackFiles> trackFiles = new ArrayList<TrackFiles>();

			for (int i = 0; i <= size; i++) {
				String[] values = res.getBody().getMessage().get(i).trim().split(",");
				for (String val : values) {
					al.add(val);
				}
			}

			logger.debug("Size " + al.size());
			for (int s = 0; s < al.size(); s += 2) {
				path = al.get(s);
				conflict_message = al.get(s + 1);
				trackFiles.add(new TrackFiles(path, conflict_message));
			}

			for (TrackFiles s : trackFiles) {
				logger.debug(s.getPath() + " " + s.getConflict_Message());
			}
			return trackFiles;
		} else {
			throw new DataNotFoundException("Project Not found");
		}
	}

	public ResponseEntity<ResponseDto> addUncontrolledFiles(TrackDto trackDto)
			throws IOException, InterruptedException {
		String projectSpec = trackDto.getProjectSpec();
		String taskId = trackDto.getTaskId();
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "reconcile", "-p", projectSpec, "-no_recurse",
				"-consider_uncontrolled", "-udb", "-task", taskId });
		return processUtility.executeProcess(p);
	}

	public ResponseEntity<ResponseDto> syncWorkAreaOfProject(String projectName)
			throws IOException, InterruptedException {
		Process p = Runtime.getRuntime().exec(new String[] { "ccm", "sync", "-r", "-s", "-p", projectName });
		return processUtility.executeProcess(p);
	}

}
```