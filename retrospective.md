# Retrospective: Avoiding Tool Errors in Workflow

## Tool & MCP Usage Instructions

1. **Use XML-style tags for all tool calls**
   Example: `<use_mcp_tool>`, `<apply_diff>`. Only actions wrapped in these tags are executed.

2. **Fill all required parameters**
   Each tool requires specific parameters (e.g., `server_name`, `path`). Omitting any required parameter will cause failure.

3. **Never use plain text for tool actions**
   Only tool-tagged actions are recognized and executed. Explanations or instructions in plain text will be ignored by the system.

4. **Wait for confirmation after each tool use**
   Always wait for the result of the previous tool before proceeding to the next step.

5. **Do not end `<attempt_completion>` with a question or further request**
   The result must be final and self-contained.

6. **For MCP tools**
   - Always specify the correct `server_name` and `tool_name`.
   - Provide all required arguments as a JSON object inside `<arguments>...</arguments>`.
   - Example:
     ```xml
     <use_mcp_tool>
       <server_name>git-mcp-server</server_name>
       <tool_name>git_status</tool_name>
       <arguments>
         {
           "path": "d:/workspace/agent-modes"
         }
       </arguments>
     </use_mcp_tool>
     ```

7. **For file operations**
   - Always provide the full file path relative to the workspace.

These rules help prevent tool errors and ensure smooth workflow execution.